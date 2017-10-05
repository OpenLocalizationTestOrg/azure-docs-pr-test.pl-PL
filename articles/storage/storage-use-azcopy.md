---
title: "Kopiowanie lub przenoszenie danych do magazynu Azure z narzędzia AzCopy w systemie Windows | Dokumentacja firmy Microsoft"
description: "W systemie AzCopy to narzędzie systemu Windows przenosić i kopiować dane do lub z obiektu blob, tabel i zawartości pliku. Kopiowanie danych do magazynu Azure z lokalnych plików lub kopiowania danych w ramach urządzeń magazynujących lub między kontami magazynu. Łatwo przeprowadzić migrację danych do usługi Azure Storage."
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
ms.openlocfilehash: 045778822022752295bb634bdf734daaf36ab938
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-the-azcopy-on-windows"></a><span data-ttu-id="3bc5e-105">Transfer danych za pomocą narzędzia AzCopy w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="3bc5e-105">Transfer data with the AzCopy on Windows</span></span>
<span data-ttu-id="3bc5e-106">Narzędzie AzCopy to narzędzie wiersza polecenia przeznaczone do kopiowania danych z magazynu obiektów Blob Microsoft Azure, plików i tabeli przy użyciu prostych poleceń z optymalną wydajnością.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-106">AzCopy is a command-line utility designed for copying data to and from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="3bc5e-107">Można skopiować danych z jednego obiektu do drugiego, w ramach konta magazynu lub między kontami magazynu.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="3bc5e-108">Istnieją dwie wersje programu AzCopy, który można pobrać.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="3bc5e-109">AzCopy w systemie Windows jest oparty na platformie .NET Framework i oferuje opcje wiersza polecenia Styl systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="3bc5e-110">[Narzędzie AzCopy w systemie Linux](storage-use-azcopy-linux.md) wbudowana w .NET Framework Core, który jest przeznaczony dla platformy Linux oferty styl POSIX opcje wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="3bc5e-111">W tym artykule omówiono AzCopy w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="3bc5e-112">Pobierz i zainstaluj narzędzie AzCopy</span><span class="sxs-lookup"><span data-stu-id="3bc5e-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="3bc5e-113">Narzędzie AzCopy w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="3bc5e-113">AzCopy on Windows</span></span>
<span data-ttu-id="3bc5e-114">Pobierz [najnowszą wersję programu AzCopy w systemie Windows](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="3bc5e-114">Download the [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="3bc5e-115">Instalacja w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="3bc5e-115">Installation on Windows</span></span>
<span data-ttu-id="3bc5e-116">Po zainstalowaniu narzędzia AzCopy w systemie Windows za pomocą Instalatora, Otwórz okno polecenia i przejdź do katalogu instalacyjnego programu AzCopy na komputerze — gdy `AzCopy.exe` wykonywalny znajduje się.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-116">After installing AzCopy on Windows using the installer, open a command window and navigate to the AzCopy installation directory on your computer - where the `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="3bc5e-117">W razie potrzeby można dodać do ścieżki systemowej lokalizacja instalacji narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-117">If desired, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="3bc5e-118">Domyślnie program AzCopy jest instalowana na `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` lub `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-118">By default, AzCopy is installed to `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="3bc5e-119">Pisanie pierwszego polecenia AzCopy</span><span class="sxs-lookup"><span data-stu-id="3bc5e-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="3bc5e-120">Podstawowa składnia polecenia AzCopy jest:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-120">The basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="3bc5e-121">W poniższych przykładach pokazano różnych scenariuszy kopiowania danych do i z programu Microsoft Azure blob, tabel i plików.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-121">The following examples demonstrate a variety of scenarios for copying data to and from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="3bc5e-122">Zapoznaj się [parametrów narzędzia AzCopy](#azcopy-parameters) sekcji, aby uzyskać szczegółowy opis parametry używane w każdej próbce.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-122">Refer to the [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="3bc5e-123">Obiekt blob: Pobierz</span><span class="sxs-lookup"><span data-stu-id="3bc5e-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="3bc5e-124">Pobieranie pojedynczego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="3bc5e-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="3bc5e-125">Należy pamiętać, że jeśli folder `C:\myfolder` nie istnieje, utworzy on i Pobierz AzCopy `abc.txt ` do nowego folderu.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-125">Note that if the folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="3bc5e-126">Pobieranie pojedynczego obiektu blob z regionu pomocniczego</span><span class="sxs-lookup"><span data-stu-id="3bc5e-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="3bc5e-127">Należy pamiętać, że użytkownik musi mieć dostęp do odczytu magazynu geograficznie nadmiarowego włączone.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="3bc5e-128">Pobierz wszystkie obiekty BLOB</span><span class="sxs-lookup"><span data-stu-id="3bc5e-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="3bc5e-129">Przyjęto założenie, że następujące obiekty BLOB znajdują się w określonym kontenerze:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-129">Assume the following blobs reside in the specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="3bc5e-130">Po wykonaniu operacji pobierania katalogu `C:\myfolder` będzie zawierać następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-130">After the download operation, the directory `C:\myfolder` will include the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="3bc5e-131">Jeśli nie zostanie określona opcja `/S`, nie obiekty BLOB zostaną pobrane.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-131">If you do not specify option `/S`, no blobs will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="3bc5e-132">Pobieranie obiektów blob z określonego prefiksu</span><span class="sxs-lookup"><span data-stu-id="3bc5e-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="3bc5e-133">Załóżmy, że następujące obiekty BLOB znajdują się w określonym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-133">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="3bc5e-134">Wszystkie obiekty BLOB rozpoczynający się od prefiksu `a` zostaną pobrane:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-134">All blobs beginning with the prefix `a` will be downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="3bc5e-135">Po wykonaniu operacji pobierania folderu `C:\myfolder` będzie zawierać następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-135">After the download operation, the folder `C:\myfolder` will include the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="3bc5e-136">Prefiks ma zastosowanie do katalogu wirtualnego, który stanowi pierwsza część nazwy obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-136">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="3bc5e-137">W przykładzie przedstawionym powyżej katalogu wirtualnego nie pasuje określony prefiks, więc nie zostanie pobrana.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-137">In the example shown above, the virtual directory does not match the specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="3bc5e-138">Ponadto jeśli opcja `\S` nie zostanie określony, narzędzie AzCopy nie będzie pobierał żadnych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-138">In addition, if the option `\S` is not specified, AzCopy will not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="3bc5e-139">Ustawianie czasu ostatniej modyfikacji plików wyeksportowane taka sama jak obiekty BLOB źródła</span><span class="sxs-lookup"><span data-stu-id="3bc5e-139">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="3bc5e-140">Można również wykluczyć obiekty BLOB z operacji pobierania na podstawie ich czasu ostatniej modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-140">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="3bc5e-141">Na przykład, jeśli chcesz wykluczyć obiekty BLOB, którego ostatniej modyfikacji jest taką samą lub nowszą niż plik docelowy Dodaj `/XN` opcji:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-141">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="3bc5e-142">Lub jeśli chcesz wykluczyć obiekty BLOB, którego ostatniej modyfikacji tego samego lub starsze niż plik docelowy Dodaj `/XO` opcji:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-142">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="3bc5e-143">Obiekt blob: Przekaż</span><span class="sxs-lookup"><span data-stu-id="3bc5e-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="3bc5e-144">Przekaż pojedynczy plik</span><span class="sxs-lookup"><span data-stu-id="3bc5e-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="3bc5e-145">Jeśli docelowy określony kontener nie istnieje, AzCopy utworzy go i przekazać go do niego.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-145">If the specified destination container does not exist, AzCopy will create it and upload the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="3bc5e-146">Przekaż pojedynczy plik do katalogu wirtualnego</span><span class="sxs-lookup"><span data-stu-id="3bc5e-146">Upload single file to virtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="3bc5e-147">Jeśli określony katalog wirtualny nie istnieje, narzędzie AzCopy przekazać pliku, aby uwzględnić w nazwie katalogu wirtualnego (*np.*, `vd/abc.txt` w powyższym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="3bc5e-147">If the specified virtual directory does not exist, AzCopy will upload the file to include the virtual directory in its name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="3bc5e-148">Przekaż wszystkie pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="3bc5e-149">Określenie opcji `/S` przekazuje rekursywnie magazynu obiektów Blob, co oznacza, że wszystkie podfoldery i pliki zostaną przekazane również zawartość określonego katalogu.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-149">Specifying option `/S` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span></span> <span data-ttu-id="3bc5e-150">Na przykład załóżmy następujące pliki znajdują się w folderze `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-150">For instance, assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="3bc5e-151">Po wykonaniu operacji przekazywania kontenera będzie zawierać następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-151">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="3bc5e-152">Jeśli nie zostanie określona opcja `/S`, AzCopy nie przekaże rekursywnie.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-152">If you do not specify option `/S`, AzCopy will not upload recursively.</span></span> <span data-ttu-id="3bc5e-153">Po wykonaniu operacji przekazywania kontenera będzie zawierać następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-153">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="3bc5e-154">Przekazywanie plików zgodnych z określonym wzorcem</span><span class="sxs-lookup"><span data-stu-id="3bc5e-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="3bc5e-155">Załóżmy następujące pliki znajdują się w folderze `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-155">Assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="3bc5e-156">Po wykonaniu operacji przekazywania kontenera będzie zawierać następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-156">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="3bc5e-157">Jeśli nie zostanie określona opcja `/S`, AzCopy przekaże tylko obiekty BLOB, które nie znajdują się w katalogu wirtualnym:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-157">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="3bc5e-158">Określ typ zawartości MIME docelowego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="3bc5e-158">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="3bc5e-159">Domyślnie narzędzie AzCopy ustawia typ zawartości do docelowego obiektu blob `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-159">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="3bc5e-160">Począwszy od wersji 3.1.0, można jawnie określić typ zawartości przy użyciu opcji `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-160">Beginning with version 3.1.0, you can explicitly specify the content type via the option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="3bc5e-161">Ta składnia ustawia typ zawartości dla wszystkich obiektów blob w operacji przekazywania.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-161">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="3bc5e-162">Jeśli określisz `/SetContentType` bez wartości, następnie AzCopy ustawi każdy obiekt blob lub typ zawartości pliku, zgodnie z jego rozszerzenie pliku.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-162">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according to its file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="3bc5e-163">Obiekt blob: kopiowania</span><span class="sxs-lookup"><span data-stu-id="3bc5e-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="3bc5e-164">Skopiuj pojedynczego obiektu blob w ramach konta magazynu</span><span class="sxs-lookup"><span data-stu-id="3bc5e-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="3bc5e-165">Podczas kopiowania obiektu blob w ramach konta magazynu, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="3bc5e-166">Skopiuj pojedynczego obiektu blob na kontach magazynu</span><span class="sxs-lookup"><span data-stu-id="3bc5e-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="3bc5e-167">Podczas kopiowania obiektu blob na kontach magazynu, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="3bc5e-168">Skopiuj pojedynczego obiektu blob z regionu pomocniczego do regionu podstawowego</span><span class="sxs-lookup"><span data-stu-id="3bc5e-168">Copy single blob from secondary region to primary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="3bc5e-169">Należy pamiętać, że użytkownik musi mieć dostęp do odczytu magazynu geograficznie nadmiarowego włączone.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="3bc5e-170">Skopiuj pojedynczego obiektu blob i jego migawek wielu kont magazynu</span><span class="sxs-lookup"><span data-stu-id="3bc5e-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="3bc5e-171">Po wykonaniu operacji kopiowania kontenera docelowego będzie zawierać obiektu blob i jego migawek.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-171">After the copy operation, the target container will include the blob and its snapshots.</span></span> <span data-ttu-id="3bc5e-172">Zakładając, że obiekt blob w powyższym przykładzie ma dwa migawki, kontenera obejmuje następujące migawki i obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-172">Assuming the blob in the example above has two snapshots, the container will include the following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="3bc5e-173">Synchronicznie skopiować wielu kont magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="3bc5e-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="3bc5e-174">Narzędzie AzCopy domyślnie kopiuje dane między dwoma punktami końcowymi magazynu asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="3bc5e-175">W związku z tym operacja kopiowania zostanie uruchomiona w tle przy użyciu pojemności nieużywanej przepustowości ma umowy dotyczącej poziomu usług pod względem jak szybko obiektu blob zostaną skopiowane, a AzCopy okresowo sprawdzać stan kopiowania, dopóki kopiowanie zakończone lub nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-175">Therefore, the copy operation will run in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check the copy status until the copying is completed or failed.</span></span>

<span data-ttu-id="3bc5e-176">`/SyncCopy` Opcja zapewnia, czy operacja kopiowania zostanie wyświetlony spójne szybkości.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-176">The `/SyncCopy` option ensures that the copy operation will get consistent speed.</span></span> <span data-ttu-id="3bc5e-177">Narzędzie AzCopy wykonuje synchroniczne kopiowania pobieranie obiektów blob można skopiować z określonego źródła do pamięci lokalnej, a następnie przekazywanie ich do miejsce docelowe magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-177">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="3bc5e-178">`/SyncCopy`może generować dodatkowe wyjście koszt w porównaniu do kopiowania asynchroniczne, zalecanym rozwiązaniem jest użycie tej opcji w maszynie Wirtualnej platformy Azure, który znajduje się w tym samym regionie co konta magazynu źródłowego, aby uniknąć kosztów wyjście.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-178">`/SyncCopy` might generate additional egress cost compared to asynchronous copy, the recommended approach is to use this option in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="3bc5e-179">Plik: Pobierz</span><span class="sxs-lookup"><span data-stu-id="3bc5e-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="3bc5e-180">Pobierz pojedynczy plik</span><span class="sxs-lookup"><span data-stu-id="3bc5e-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="3bc5e-181">Jeśli określone źródło jest udział plików na platformę Azure, a następnie podaj nazwę pliku dokładną (*np.* `abc.txt`) do pobrania pojedynczy plik, lub określ opcję `/S` Aby pobrać wszystkie pliki w udziale rekursywnie.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-181">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `/S` to download all files in the share recursively.</span></span> <span data-ttu-id="3bc5e-182">Podjęto próbę Określ wzorzec pliku i opcji `/S` razem spowoduje wystąpienie błędu.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-182">Attempting to specify both a file pattern and option `/S` together will result in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="3bc5e-183">Pobierz wszystkie pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="3bc5e-184">Uwaga puste foldery nie zostaną pobrane.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-184">Note that any empty folders will not be downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="3bc5e-185">Plik: Przekaż</span><span class="sxs-lookup"><span data-stu-id="3bc5e-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="3bc5e-186">Przekaż pojedynczy plik</span><span class="sxs-lookup"><span data-stu-id="3bc5e-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="3bc5e-187">Przekaż wszystkie pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="3bc5e-188">Uwaga puste foldery nie zostaną przekazane.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-188">Note that any empty folders will not be uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="3bc5e-189">Przekazywanie plików zgodnych z określonym wzorcem</span><span class="sxs-lookup"><span data-stu-id="3bc5e-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="3bc5e-190">Plik: kopiowania</span><span class="sxs-lookup"><span data-stu-id="3bc5e-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="3bc5e-191">Kopiowanie między udziałami plików</span><span class="sxs-lookup"><span data-stu-id="3bc5e-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="3bc5e-192">Podczas kopiowania plików między udziałami plików [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="3bc5e-193">Kopiowanie z udziału plików do obiektu blob</span><span class="sxs-lookup"><span data-stu-id="3bc5e-193">Copy from file share to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="3bc5e-194">Podczas kopiowania pliku z udziału plików do obiektów blob, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-194">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="3bc5e-195">Kopiowanie z obiektu blob do udziału plików</span><span class="sxs-lookup"><span data-stu-id="3bc5e-195">Copy from blob to file share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="3bc5e-196">Podczas kopiowania pliku z obiektu blob do udziału plików, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-196">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="3bc5e-197">Synchronicznie kopiować pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-197">Synchronously copy files</span></span>
<span data-ttu-id="3bc5e-198">Można określić `/SyncCopy` opcję, aby skopiować dane z pliku magazynu do przechowywania plików, z pliku magazynu do magazynu obiektów Blob i z magazynu obiektów Blob do przechowywania plików synchronicznie, AzCopy przez pobieranie źródła danych do pamięci lokalnej i ponownie przekazać go do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-198">You can specify the `/SyncCopy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously, AzCopy does this by downloading the source data to local memory and upload it again to destination.</span></span> <span data-ttu-id="3bc5e-199">Wyjście standardowe koszt będą stosowane.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-199">Standard egress cost will apply.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="3bc5e-200">Podczas kopiowania z pliku magazynu do magazynu obiektów Blob, domyślnym typem obiektu blob jest blokowych obiektów blob, użytkownik może określić opcję `/BlobType:page` zmienić typ docelowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-200">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="3bc5e-201">Należy pamiętać, że `/SyncCopy` może generować wyjście dodatkowych kosztów porównanie kopii asynchroniczne, zalecanym rozwiązaniem jest użycie tej opcji w maszynie Wirtualnej platformy Azure, który znajduje się w tym samym regionie co konta magazynu źródłowego, aby uniknąć kosztów wyjście.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-201">Note that `/SyncCopy` might generate additional egress cost comparing to asynchronous copy, the recommended approach is to use this option in the Azure VM which is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="3bc5e-202">Tabela: eksportowanie</span><span class="sxs-lookup"><span data-stu-id="3bc5e-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="3bc5e-203">Eksportowanie tabeli</span><span class="sxs-lookup"><span data-stu-id="3bc5e-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="3bc5e-204">Narzędzie AzCopy zapisuje plik manifestu do folderu określonej lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-204">AzCopy writes a manifest file to the specified destination folder.</span></span> <span data-ttu-id="3bc5e-205">Plik manifestu jest używany w procesie importu do lokalizowania plików niezbędnych danych i sprawdzania poprawności danych.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-205">The manifest file is used in the import process to locate the necessary data files and perform data validation.</span></span> <span data-ttu-id="3bc5e-206">Domyślnie plik manifestu używa następującej konwencji nazewnictwa:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-206">The manifest file uses the following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="3bc5e-207">Użytkownik może również określić opcję `/Manifest:<manifest file name>` można ustawić nazwy pliku manifestu.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-207">User can also specify the option `/Manifest:<manifest file name>` to set the manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="3bc5e-208">Eksport podzielonego na wiele plików</span><span class="sxs-lookup"><span data-stu-id="3bc5e-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="3bc5e-209">Korzysta z narzędzia AzCopy *indeksu woluminu* w nazwach plików danych podziału celu rozróżnienia wielu plików.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-209">AzCopy uses a *volume index* in the split data file names to distinguish multiple files.</span></span> <span data-ttu-id="3bc5e-210">Indeks woluminu składa się z dwóch części *indeksu zakresem kluczy partycji* i *podziału pliku indeksu*.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-210">The volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="3bc5e-211">Zarówno indeksy są liczony od zera.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="3bc5e-212">Indeks zakresem kluczy partycji będzie równa 0, jeśli użytkownik nie określi opcji `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-212">The partition key range index will be 0 if user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="3bc5e-213">Na przykład, załóżmy, że AzCopy generuje dwa pliki danych po użytkownika określa opcję `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-213">For instance, suppose AzCopy generates two data files after the user specifies option `/SplitSize`.</span></span> <span data-ttu-id="3bc5e-214">Wynikowa nazwy pliku danych może być:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-214">The resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="3bc5e-215">Należy pamiętać, że minimalna możliwych wartości dla opcji `/SplitSize` wynosi 32 MB.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-215">Note that the minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="3bc5e-216">Jeśli określone miejsce docelowe magazynu obiektów Blob, AzCopy będzie dzielenie pliku danych, po jego rozmiary przez nią miejsce osiągnie limit rozmiaru obiektów blob (200GB), niezależnie od tego, czy opcja `/SplitSize` został określony przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-216">If the specified destination is Blob storage, AzCopy will split the data file once its sizes reaches the blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by the user.</span></span>

### <a name="export-table-to-json-or-csv-data-file-format"></a><span data-ttu-id="3bc5e-217">Eksportowanie tabeli na format pliku danych JSON lub CSV</span><span class="sxs-lookup"><span data-stu-id="3bc5e-217">Export table to JSON or CSV data file format</span></span>
<span data-ttu-id="3bc5e-218">Narzędzie AzCopy domyślnie eksportuje tabel do plików danych JSON.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-218">AzCopy by default exports tables to JSON data files.</span></span> <span data-ttu-id="3bc5e-219">Można określić opcję `/PayloadFormat:JSON|CSV` Eksportowanie tabel jako JSON lub CSV.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-219">You can specify the option `/PayloadFormat:JSON|CSV` to export the tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="3bc5e-220">Podczas określania format ładunku CSV, AzCopy również wygeneruje plik schematu z rozszerzeniem pliku `.schema.csv` dla każdego pliku danych.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-220">When specifying the CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="3bc5e-221">Eksportowanie tabeli jednocześnie jednostek</span><span class="sxs-lookup"><span data-stu-id="3bc5e-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="3bc5e-222">Narzędzie AzCopy rozpocznie jednoczesnych operacji eksportowania jednostek, gdy użytkownik określi opcji `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-222">AzCopy will start concurrent operations to export entities when the user specifies option `/PKRS`.</span></span> <span data-ttu-id="3bc5e-223">Każda operacja eksportuje jednym zakresem kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="3bc5e-224">Należy pamiętać, że liczba jednoczesnych operacji również jest kontrolowane przez opcję `/NC`.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-224">Note that the number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="3bc5e-225">AzCopy używa liczba rdzeni procesorów jako wartość domyślną `/NC` podczas kopiowania jednostek tabeli, nawet jeśli `/NC` nie została określona.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-225">AzCopy uses the number of core processors as the default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="3bc5e-226">Gdy użytkownik określi opcji `/PKRS`, AzCopy używa mniejszej z dwóch wartości — zakresami kluczy partycji i jawnie lub niejawnie określono jednoczesnych operacji — do określić liczbę jednoczesnych operacji można uruchomić.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-226">When the user specifies option `/PKRS`, AzCopy uses the smaller of the two values - partition key ranges versus implicitly or explicitly specified concurrent operations - to determine the number of concurrent operations to start.</span></span> <span data-ttu-id="3bc5e-227">Aby uzyskać więcej informacji, wpisz `AzCopy /?:NC` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-227">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="export-table-to-blob"></a><span data-ttu-id="3bc5e-228">Eksportowanie tabeli do obiektu blob</span><span class="sxs-lookup"><span data-stu-id="3bc5e-228">Export table to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="3bc5e-229">Narzędzie AzCopy wygeneruje plik danych JSON do kontenera obiektów blob z następującą konwencją:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-229">AzCopy will generate a JSON data file into the blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="3bc5e-230">Wygenerowany plik danych JSON następuje format ładunku dla minimalne metadane.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-230">The generated JSON data file follows the payload format for minimal metadata.</span></span> <span data-ttu-id="3bc5e-231">Aby uzyskać więcej informacji na ten format ładunku, zobacz [Format ładunku dla operacji usługi tabeli](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="3bc5e-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="3bc5e-232">Należy pamiętać, że podczas eksportowania tabel do obiektów blob, AzCopy będzie pobrać jednostek tabeli na pliki tymczasowe dane lokalne, a następnie przekaż te jednostki do obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-232">Note that when exporting tables to blobs, AzCopy will download the Table entities to local temporary data files and then upload those entities to the blob.</span></span> <span data-ttu-id="3bc5e-233">Te dane tymczasowe pliki są umieszczane w folder plików dziennika z domyślnej ścieżki "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", można określić opcję/Z: [arkusza pliku folder] do dziennika zmian lokalizacja folderu pliku i w związku z tym zmienić lokalizację plików danych tymczasowych.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-233">These temporary data files are put into the journal file folder with the default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] to change the journal file folder location and thus change the temporary data files location.</span></span> <span data-ttu-id="3bc5e-234">Zadecyduje o rozmiar jednostek tabeli i rozmiar określony /SplitSize — opcja rozmiaru plików danych tymczasowych, chociaż plik danych tymczasowych dysku lokalnego zostaną usunięte natychmiast po przekazaniu obiektu blob, upewnij się, że masz wystarczającą ilość miejsca na dysku do przechowywania plików tymczasowych danych, przed usunięciem.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-234">The temporary data files' size is decided by your table entities' size and the size you specified with the option /SplitSize, although the temporary data file in local disk will be deleted instantly once it has been uploaded to the blob, please make sure you have enough local disk space to store these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="3bc5e-235">Tabela: Import</span><span class="sxs-lookup"><span data-stu-id="3bc5e-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="3bc5e-236">Importowanie tabeli</span><span class="sxs-lookup"><span data-stu-id="3bc5e-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="3bc5e-237">Opcja `/EntityOperation` wskazuje sposób wstawiania jednostek do tabeli.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-237">The option `/EntityOperation` indicates how to insert entities into the table.</span></span> <span data-ttu-id="3bc5e-238">Możliwe wartości:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-238">Possible values are:</span></span>

* <span data-ttu-id="3bc5e-239">`InsertOrSkip`: Pomija istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="3bc5e-240">`InsertOrMerge`: Scala istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="3bc5e-241">`InsertOrReplace`: Zastępuje istniejące jednostki i wstawia nową jednostkę, jeśli nie istnieje w tabeli.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="3bc5e-242">Zauważ, że nie można określić opcji `/PKRS` w scenariuszu importu.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-242">Note that you cannot specify option `/PKRS` in the import scenario.</span></span> <span data-ttu-id="3bc5e-243">W odróżnieniu od scenariusza eksportu, w którym należy określić opcję `/PKRS` zacząć jednoczesnych operacji AzCopy domyślnie rozpocznie jednoczesnych operacji importowania tabeli.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-243">Unlike the export scenario, in which you must specify option `/PKRS` to start concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span></span> <span data-ttu-id="3bc5e-244">Domyślna liczba jednoczesnych operacji uruchomiona jest równa liczbie procesorów; jednak można określić różne liczby równoczesnych z opcją `/NC`.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-244">The default number of concurrent operations started is equal to the number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="3bc5e-245">Aby uzyskać więcej informacji, wpisz `AzCopy /?:NC` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-245">For more details, type `AzCopy /?:NC` at the command line.</span></span>

<span data-ttu-id="3bc5e-246">Należy pamiętać, że narzędzie AzCopy obsługuje wyłącznie importowanie do formatu JSON, CSV nie.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="3bc5e-247">AzCopy nie obsługuje importowania tabeli z JSON utworzonych przez użytkownika i pliki manifestu.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="3bc5e-248">Oba te pliki muszą pochodzić z narzędzia AzCopy tabeli eksportu.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="3bc5e-249">Aby uniknąć błędów, nie zmodyfikuj wyeksportowanego JSON lub pliku manifestu.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-249">To avoid errors, please do not modify the exported JSON or manifest file.</span></span>

### <a name="import-entities-to-table-using-blobs"></a><span data-ttu-id="3bc5e-250">Importowanie jednostek do tabeli, używając obiektów blob</span><span class="sxs-lookup"><span data-stu-id="3bc5e-250">Import entities to table using blobs</span></span>
<span data-ttu-id="3bc5e-251">Założono kontenera obiektów Blob zawiera następujące: plik A JSON reprezentujący tabel Azure i jego towarzyszący plik manifestu.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-251">Assume a Blob container contains the following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="3bc5e-252">Można uruchomić następujące polecenie, aby zaimportować jednostki do tabeli za pomocą pliku manifestu w danym kontenerze obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-252">You can run the following command to import entities into a table using the manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="3bc5e-253">Inne funkcje AzCopy</span><span class="sxs-lookup"><span data-stu-id="3bc5e-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="3bc5e-254">Tylko skopiować dane, które nie istnieje w docelowym</span><span class="sxs-lookup"><span data-stu-id="3bc5e-254">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="3bc5e-255">`/XO` i `/XN` parametry umożliwiają Wyklucz zasoby starszej lub nowszej źródła zapobiega kopiowaniu odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-255">The `/XO` and `/XN` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="3bc5e-256">Jeśli chcesz skopiować źródła zasobów, które nie istnieje w docelowym, można określić oba parametry polecenia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-256">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="3bc5e-257">Należy pamiętać, że to nie jest obsługiwana podczas źródłowe lub docelowe jest tabelą.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-257">Note that this is not supported when either the source or destination is a table.</span></span>

### <a name="use-a-response-file-to-specify-command-line-parameters"></a><span data-ttu-id="3bc5e-258">Określ parametry wiersza polecenia przy użyciu pliku odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3bc5e-258">Use a response file to specify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="3bc5e-259">Parametry wiersza polecenia AzCopy można umieścić w pliku odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="3bc5e-260">Narzędzie AzCopy przetwarza parametrów w pliku tak, jakby były one określone w wierszu polecenia wykonywanie bezpośrednich podstawienia z zawartością pliku.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-260">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="3bc5e-261">Załóżmy, plik odpowiedzi o nazwie `copyoperation.txt`, który zawiera następujące wiersze.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-261">Assume a response file named `copyoperation.txt`, that contains the following lines.</span></span> <span data-ttu-id="3bc5e-262">Każdy parametr narzędzia AzCopy można określić w jednym wierszu</span><span class="sxs-lookup"><span data-stu-id="3bc5e-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="3bc5e-263">lub na oddzielnych wierszach:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="3bc5e-264">Narzędzie AzCopy zakończy się niepowodzeniem, jeśli parametr można podzielić na dwa wiersze, jak pokazano poniżej, aby uzyskać `/sourcekey` parametru:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-264">AzCopy will fail if you split the parameter across two lines, as shown here for the `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-to-specify-command-line-parameters"></a><span data-ttu-id="3bc5e-265">Użyj wielu plików odpowiedzi, aby określić parametry wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="3bc5e-265">Use multiple response files to specify command-line parameters</span></span>
<span data-ttu-id="3bc5e-266">Załóżmy, plik odpowiedzi o nazwie `source.txt` , który określa kontener źródła:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="3bc5e-267">I plik odpowiedzi o nazwie `dest.txt` określający folderu docelowego w systemie plików:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-267">And a response file named `dest.txt` that specifies a destination folder in the file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="3bc5e-268">I plik odpowiedzi o nazwie `options.txt` , który określa opcje narzędzia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="3bc5e-269">Aby wywołać narzędzia AzCopy z tych plików odpowiedzi, które znajdują się w katalogu `C:\responsefiles`, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-269">To call AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="3bc5e-270">Narzędzie AzCopy przetwarza to polecenie tak samo, jak gdyby uwzględnione wszystkie poszczególne parametry w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-270">AzCopy processes this command just as it would if you included all of the individual parameters on the command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="3bc5e-271">Określ sygnatury dostępu współdzielonego (SAS)</span><span class="sxs-lookup"><span data-stu-id="3bc5e-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="3bc5e-272">Można również określić sygnatury dostępu Współdzielonego w kontenerze identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-272">You can also specify a SAS on the container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="3bc5e-273">Folder plików dziennika</span><span class="sxs-lookup"><span data-stu-id="3bc5e-273">Journal file folder</span></span>
<span data-ttu-id="3bc5e-274">Zawsze, gdy wydać polecenie do narzędzia AzCopy, sprawdza czy istnieje w pliku dziennika w domyślnym folderze, lub czy istnieje w folderze określonej za pomocą tej opcji.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-274">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="3bc5e-275">Jeśli plik dziennika nie istnieje w każdym miejscu, AzCopy traktuje jako nowe działanie i generuje nowy plik dziennika.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-275">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="3bc5e-276">Jeśli plik dziennika istnieje, narzędzie AzCopy sprawdzi, czy wiersz polecenia, który możesz wpisać zgodny wiersz polecenia w pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-276">If the journal file does exist, AzCopy will check whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="3bc5e-277">Jeśli dwa wiersze poleceń są zgodne, AzCopy wznawia działanie niekompletne.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-277">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="3bc5e-278">Jeśli nie są zgodne, pojawi się monit o albo zastąpienie pliku dziennika można uruchomić nowej operacji lub Anuluj bieżącą operację.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-278">If they do not match, you will be prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="3bc5e-279">Jeśli chcesz użyć domyślnej lokalizacji pliku dziennika:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-279">If you want to use the default location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="3bc5e-280">Jeśli pominięto opcję `/Z`, lub określ opcję `/Z` bez ścieżkę do folderu, jak pokazano powyżej, AzCopy tworzy plik dziennika w lokalizacji domyślnej, która jest `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-280">If you omit option `/Z`, or specify option `/Z` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="3bc5e-281">Jeśli istnieje już plik dziennika, AzCopy wznawia działanie na podstawie pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-281">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="3bc5e-282">Jeśli chcesz określić niestandardową lokalizację pliku dziennika:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-282">If you want to specify a custom location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="3bc5e-283">W tym przykładzie powoduje utworzenie pliku dziennika, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-283">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="3bc5e-284">Jeśli istnieje, narzędzie AzCopy wznawia działanie na podstawie pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-284">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="3bc5e-285">Jeśli chcesz wznowić działanie narzędzia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-285">If you want to resume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="3bc5e-286">W tym przykładzie wznawia Ostatnia operacja mogła zakończyć się niepowodzeniem, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-286">This example resumes the last operation, which may have failed to complete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="3bc5e-287">Wygenerowanie pliku dziennika</span><span class="sxs-lookup"><span data-stu-id="3bc5e-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="3bc5e-288">Jeśli określono opcję `/V` bez podawania ścieżkę pliku do pełnego dziennika, następnie AzCopy tworzy plik dziennika w lokalizacji domyślnej, która jest `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-288">If you specify option `/V` without providing a file path to the verbose log, then AzCopy creates the log file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="3bc5e-289">W przeciwnym razie należy utworzyć plik dziennika w lokalizacji niestandardowej:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="3bc5e-290">Należy pamiętać, że jeśli Określ ścieżkę względną po opcji `/V`, takich jak `/V:test/azcopy1.log`, a następnie pełnego dziennika jest tworzony w bieżącym katalogu roboczym w podfolderze o nazwie `test`.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then the verbose log is created in the current working directory within a subfolder named `test`.</span></span>

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="3bc5e-291">Określ liczbę jednoczesnych operacji można uruchomić</span><span class="sxs-lookup"><span data-stu-id="3bc5e-291">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="3bc5e-292">Opcja `/NC` określa liczbę jednoczesnych kopii operacji.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-292">Option `/NC` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="3bc5e-293">Domyślnie narzędzie AzCopy uruchamia określonej liczby jednoczesnych operacji w celu zwiększenia przepływności transferu danych.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-293">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="3bc5e-294">Operacjach tabeli liczba jednoczesnych operacji jest równa liczbie procesorów, które masz.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-294">For Table operations, the number of concurrent operations is equal to the number of processors you have.</span></span> <span data-ttu-id="3bc5e-295">Dla operacji obiektów Blob i pliku, liczba jednoczesnych operacji jest równa 8 razy liczba procesorów posiadanego.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-295">For Blob and File operations, the number of concurrent operations is equal 8 times the number of processors you have.</span></span> <span data-ttu-id="3bc5e-296">Jeśli używasz narzędzia AzCopy w niskiej przepustowości sieci, można określić mniejszą liczbę dla /NC uniknąć błąd spowodowany konkurencji zasobów.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC to avoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="3bc5e-297">Uruchom narzędzie AzCopy dla emulatora magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="3bc5e-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="3bc5e-298">Możesz uruchomić narzędzie AzCopy przed [emulatora magazynu Azure](storage-use-emulator.md) dla obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-298">You can run AzCopy against the [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="3bc5e-299">i tabele:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="3bc5e-300">Parametry AzCopy</span><span class="sxs-lookup"><span data-stu-id="3bc5e-300">AzCopy Parameters</span></span>
<span data-ttu-id="3bc5e-301">Poniżej opisano parametry narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="3bc5e-302">Można również wpisać jedną z następujących poleceń z poziomu wiersza polecenia, aby uzyskać pomoc przy użyciu narzędzia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-302">You can also type one of the following commands from the command line for help in using AzCopy:</span></span>

* <span data-ttu-id="3bc5e-303">Aby uzyskać szczegółową pomoc wiersza polecenia AzCopy:`AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="3bc5e-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="3bc5e-304">Szczegółowe informacje o żadnych parametrów narzędzia AzCopy:`AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="3bc5e-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="3bc5e-305">Przykłady wiersza polecenia:`AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="3bc5e-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="3bc5e-306">/ Źródła: "source"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-306">/Source:"source"</span></span>
<span data-ttu-id="3bc5e-307">Określa źródło danych do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-307">Specifies the source data from which to copy.</span></span> <span data-ttu-id="3bc5e-308">Źródło może być katalogu w systemie plików, kontenera obiektów blob, katalog wirtualny obiektów blob, udział pliku magazynu, katalog pliku magazynu lub tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-308">The source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="3bc5e-309">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="3bc5e-310">/ Dest: "miejsce docelowe"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-310">/Dest:"destination"</span></span>
<span data-ttu-id="3bc5e-311">Określa miejsce docelowe kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-311">Specifies the destination to copy to.</span></span> <span data-ttu-id="3bc5e-312">Miejsce docelowe może być katalogu w systemie plików, kontenera obiektów blob, katalog wirtualny obiektów blob, udział pliku magazynu, katalog pliku magazynu lub tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-312">The destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="3bc5e-313">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="3bc5e-314">/ Wzorca: "wzorzec pliku"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="3bc5e-315">Określa wzorzec pliku, która wskazuje plików do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-315">Specifies a file pattern that indicates which files to copy.</span></span> <span data-ttu-id="3bc5e-316">Zachowanie parametru /Pattern zależy od lokalizacji źródła danych i obecności w trybie cykliczne.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-316">The behavior of the /Pattern parameter is determined by the location of the source data, and the presence of the recursive mode option.</span></span> <span data-ttu-id="3bc5e-317">Za pomocą opcji opcji/s. jest określony tryb cykliczne</span><span class="sxs-lookup"><span data-stu-id="3bc5e-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="3bc5e-318">Jeśli określone źródło jest katalogiem w systemie plików, a następnie obowiązują standardowe symbole wieloznaczne i podać wzorzec pliku jest dopasowywana do plików w katalogu.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-318">If the specified source is a directory in the file system, then standard wildcards are in effect, and the file pattern provided is matched against files within the directory.</span></span> <span data-ttu-id="3bc5e-319">Jeśli opcja/s jest określana, następnie AzCopy zgodny określony wzorzec względem wszystkich plików w wszystkie podfoldery znajdujące się poniżej katalogu.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-319">If option /S is specified, then AzCopy also matches the specified pattern against all files in any subfolders beneath the directory.</span></span>

<span data-ttu-id="3bc5e-320">Jeśli określone źródło jest kontenera obiektów blob lub katalogu wirtualnego, symbole wieloznaczne nie są stosowane.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-320">If the specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="3bc5e-321">Jeśli opcja/s jest określana, następnie AzCopy interpretuje wzorzec określony plik jako prefiks obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-321">If option /S is specified, then AzCopy interprets the specified file pattern as a blob prefix.</span></span> <span data-ttu-id="3bc5e-322">Jeśli opcja /S nie zostanie określony, następnie AzCopy zgodny z wzorcem pliku nazwami dokładne obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-322">If option /S is not specified, then AzCopy matches the file pattern against exact blob names.</span></span>

<span data-ttu-id="3bc5e-323">Jeśli określone źródło jest udział plików na platformę Azure, należy określić nazwę pliku dokładne, (np. abc.txt) do skopiowania pojedynczy plik, lub określ opcję/s do skopiowania wszystkich plików w udziale rekursywnie.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-323">If the specified source is an Azure file share, then you must either specify the exact file name, (e.g. abc.txt) to copy a single file, or specify option /S to copy all files in the share recursively.</span></span> <span data-ttu-id="3bc5e-324">Próby Określ wzorzec pliku i opcji /S razem spowoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-324">Attempting to specify both a file pattern and option /S together will result in an error.</span></span>

<span data-ttu-id="3bc5e-325">AzCopy korzysta z uwzględnieniem wielkości liter dopasowanie, jeśli / Source jest kontenera obiektów blob lub katalogu wirtualnego obiektów blob i korzysta z odpowiadającym bez uwzględniania wielkości liter we wszystkich innych przypadkach.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-325">AzCopy uses case-sensitive matching when the /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all the other cases.</span></span>

<span data-ttu-id="3bc5e-326">Plik domyślny wzorzec używany, jeśli nie określono żadnych wzorzec pliku jest *.*</span><span class="sxs-lookup"><span data-stu-id="3bc5e-326">The default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="3bc5e-327">dla lokalizacji systemu plików lub pustego prefiksu lokalizacji magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="3bc5e-328">Nie można określać wielu wzorców pliku.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="3bc5e-329">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="3bc5e-330">/ DestKey: "klucz magazynu"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="3bc5e-331">Określa klucz konta magazynu dla zasobu docelowego.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-331">Specifies the storage account key for the destination resource.</span></span>

<span data-ttu-id="3bc5e-332">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="3bc5e-333">/ DestSAS: "tokenu sygnatury dostępu współdzielonego"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="3bc5e-334">Określa dostępu sygnatury dostępu Współdzielonego z uprawnieniami odczytu i zapisu dla miejsca docelowego (jeśli dotyczy).</span><span class="sxs-lookup"><span data-stu-id="3bc5e-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for the destination (if applicable).</span></span> <span data-ttu-id="3bc5e-335">Ująć SAS z cudzysłowami podwójnymi, jak mogą zawiera znaki specjalne wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-335">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="3bc5e-336">Zasób docelowy jest kontenera obiektów blob, udziału plików lub tabeli, można określić tę opcję, a następnie tokenu sygnatury dostępu Współdzielonego, czy jako element docelowy kontener obiektów blob, udziału plików lub tabeli identyfikatora URI, bez tej opcji można określić sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-336">If the destination resource is a blob container, file share or table, you can either specify this option followed by the SAS token, or you can specify the SAS as part of the destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="3bc5e-337">Jeśli na źródłowym i docelowym są oba obiekty BLOB, docelowego obiektu blob musi znajdować się w tym samym kontem magazynu obiektów blob źródła.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-337">If the source and destination are both blobs, then the destination blob must reside within the same storage account as the source blob.</span></span>

<span data-ttu-id="3bc5e-338">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="3bc5e-339">/ SourceKey: "klucz magazynu"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="3bc5e-340">Określa klucz konta magazynu dla zasobu źródła.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-340">Specifies the storage account key for the source resource.</span></span>

<span data-ttu-id="3bc5e-341">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="3bc5e-342">/ SourceSAS: "tokenu sygnatury dostępu współdzielonego"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="3bc5e-343">Określa sygnaturę dostępu współdzielonego z uprawnieniami odczytu i listy dla źródła (jeśli dotyczy).</span><span class="sxs-lookup"><span data-stu-id="3bc5e-343">Specifies a Shared Access Signature with READ and LIST permissions for the source (if applicable).</span></span> <span data-ttu-id="3bc5e-344">Ująć SAS z cudzysłowami podwójnymi, jak mogą zawiera znaki specjalne wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-344">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="3bc5e-345">Jeśli zasób źródła jest kontenera obiektów blob, a podano klucz ani sygnatury dostępu Współdzielonego, za pomocą anonimowego dostępu do odczytu jest kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-345">If the source resource is a blob container, and neither a key nor a SAS is provided, then the blob container will be read via anonymous access.</span></span>

<span data-ttu-id="3bc5e-346">Jeśli źródło jest udział plików lub tabeli, należy podać klucz lub sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-346">If the source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="3bc5e-347">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="3bc5e-348">/ S</span><span class="sxs-lookup"><span data-stu-id="3bc5e-348">/S</span></span>
<span data-ttu-id="3bc5e-349">Określa tryb cyklicznych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="3bc5e-350">W trybie cykliczne AzCopy zostaną skopiowane wszystkie obiekty BLOB lub pliki, które jest zgodny z wzorcem określonego pliku, włącznie z zawartymi w podfolderach.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-350">In recursive mode, AzCopy will copy all blobs or files that match the specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="3bc5e-351">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="3bc5e-352">/ BlobType: "block" | "page" | "Dołącz"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="3bc5e-353">Określa, czy docelowego obiektu blob jest blokowych obiektów blob i stronicowych obiektów blob, uzupełnialny obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-353">Specifies whether the destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="3bc5e-354">Ta opcja ma zastosowanie tylko wtedy, gdy przekazujesz obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="3bc5e-355">W przeciwnym razie zostanie wygenerowany błąd.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="3bc5e-356">Jeśli obiektem docelowym jest obiektu blob, a ta opcja nie jest określona, domyślnie AzCopy tworzy blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-356">If the destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="3bc5e-357">**Dotyczy:** obiektów blob</span><span class="sxs-lookup"><span data-stu-id="3bc5e-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="3bc5e-358">/ CheckMD5</span><span class="sxs-lookup"><span data-stu-id="3bc5e-358">/CheckMD5</span></span>
<span data-ttu-id="3bc5e-359">Oblicza Skrót MD5 danych pobrane i weryfikuje, czy skrótu MD5 przechowywana w obiekcie blob lub właściwość Content-MD5 pliku odpowiada obliczona wartość skrótu.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-359">Calculates an MD5 hash for downloaded data and verifies that the MD5 hash stored in the blob or file's Content-MD5 property matches the calculated hash.</span></span> <span data-ttu-id="3bc5e-360">Wyboru MD5 jest domyślnie wyłączona, dlatego należy określić tę opcję, aby sprawdzić MD5 podczas pobierania danych.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-360">The MD5 check is turned off by default, so you must specify this option to perform the MD5 check when downloading data.</span></span>

<span data-ttu-id="3bc5e-361">Należy pamiętać, że usługi Azure Storage nie gwarantuje, że skrótu MD5 przechowywane dla obiekt blob, czy plik jest aktualny.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-361">Note that Azure Storage doesn't guarantee that the MD5 hash stored for the blob or file is up-to-date.</span></span> <span data-ttu-id="3bc5e-362">Odpowiada klienta MD5 aktualizowania obiektów blob lub plik jest modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-362">It is client's responsibility to update the MD5 whenever the blob or file is modified.</span></span>

<span data-ttu-id="3bc5e-363">Narzędzie AzCopy zawsze ustawia właściwość Content-MD5 dla pliku lub obiektów blob platformy Azure po przekazać go do usługi.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-363">AzCopy always sets the Content-MD5 property for an Azure blob or file after uploading it to the service.</span></span>  

<span data-ttu-id="3bc5e-364">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="3bc5e-365">/ Migawki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-365">/Snapshot</span></span>
<span data-ttu-id="3bc5e-366">Wskazuje, czy należy przesłać migawki.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-366">Indicates whether to transfer snapshots.</span></span> <span data-ttu-id="3bc5e-367">Ta opcja jest prawidłowy tylko w przypadku, gdy źródłem jest obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-367">This option is only valid when the source is a blob.</span></span>

<span data-ttu-id="3bc5e-368">Migawki obiektu blob przekazanych zostały zmienione w następującym formacie: .extension nazwy obiektów blob (migawka time)</span><span class="sxs-lookup"><span data-stu-id="3bc5e-368">The transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="3bc5e-369">Domyślnie nie są kopiowane migawki.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="3bc5e-370">**Dotyczy:** obiektów blob</span><span class="sxs-lookup"><span data-stu-id="3bc5e-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="3bc5e-371">/ V: [plików pełnego dziennika]</span><span class="sxs-lookup"><span data-stu-id="3bc5e-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="3bc5e-372">Komunikaty stanu pełne dane wyjściowe do pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="3bc5e-373">Domyślnie plik dziennika pełne nosi nazwę AzCopyVerbose.log w `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-373">By default, the verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="3bc5e-374">Jeśli określisz istniejącej lokalizacji plików dla tej opcji pełnego dziennika zostaną dodane do tego pliku.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-374">If you specify an existing file location for this option, the verbose log will be appended to that file.</span></span>  

<span data-ttu-id="3bc5e-375">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="3bc5e-376">/ Z: [arkusza pliku folder]</span><span class="sxs-lookup"><span data-stu-id="3bc5e-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="3bc5e-377">Określa folder plików dziennika dla wznawia działanie.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="3bc5e-378">Narzędzie AzCopy zawsze obsługuje wznawianie, jeśli operacja została przerwana.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="3bc5e-379">Jeśli ta opcja nie jest określony lub został określony bez ścieżki folderu, AzCopy spowoduje utworzenie pliku dziennika w lokalizacji domyślnej, czyli % LocalAppData%\Microsoft\Azure\AzCopy.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-379">If this option is not specified, or it is specified without a folder path, then AzCopy will create the journal file in the default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="3bc5e-380">Zawsze, gdy wydać polecenie do narzędzia AzCopy, sprawdza czy istnieje w pliku dziennika w domyślnym folderze, lub czy istnieje w folderze określonej za pomocą tej opcji.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-380">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="3bc5e-381">Jeśli plik dziennika nie istnieje w każdym miejscu, AzCopy traktuje jako nowe działanie i generuje nowy plik dziennika.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-381">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="3bc5e-382">Jeśli plik dziennika istnieje, narzędzie AzCopy sprawdzi, czy wiersz polecenia, który możesz wpisać zgodny wiersz polecenia w pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-382">If the journal file does exist, AzCopy will check whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="3bc5e-383">Jeśli dwa wiersze poleceń są zgodne, AzCopy wznawia działanie niekompletne.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-383">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="3bc5e-384">Jeśli nie są zgodne, pojawi się monit o albo zastąpienie pliku dziennika można uruchomić nowej operacji lub Anuluj bieżącą operację.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-384">If they do not match, you will be prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="3bc5e-385">Plik dziennika jest usuwany po pomyślnym zakończeniu operacji.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-385">The journal file is deleted upon successful completion of the operation.</span></span>

<span data-ttu-id="3bc5e-386">Należy pamiętać, że wznawia działanie z pliku dziennika utworzonego przez poprzednią wersję programu AzCopy nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="3bc5e-387">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="3bc5e-388">/@:"parameter-File"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-388">/@:"parameter-file"</span></span>
<span data-ttu-id="3bc5e-389">Określa plik, który zawiera parametry.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="3bc5e-390">Narzędzie AzCopy przetwarza parametrów w pliku, tak jakby były one określone w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-390">AzCopy processes the parameters in the file just as if they had been specified on the command line.</span></span>

<span data-ttu-id="3bc5e-391">W pliku odpowiedzi można określić wiele parametrów w jednym wierszu lub określ każdego parametru w osobnym wierszu.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="3bc5e-392">Należy pamiętać, że poszczególne parametru nie może obejmować wiele wierszy.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="3bc5e-393">Pliki odpowiedzi mogą obejmować komentarze wierszy, które zaczynają się od symbolu #.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-393">Response files can include comments lines that begin with the # symbol.</span></span>

<span data-ttu-id="3bc5e-394">Można określić wiele plików odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-394">You can specify multiple response files.</span></span> <span data-ttu-id="3bc5e-395">Jednak należy pamiętać, że narzędzie AzCopy nie obsługuje zagnieżdżone pliki odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="3bc5e-396">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="3bc5e-397">/ Y</span><span class="sxs-lookup"><span data-stu-id="3bc5e-397">/Y</span></span>
<span data-ttu-id="3bc5e-398">Pomija wszystkie monity potwierdzenie narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="3bc5e-399">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="3bc5e-400">/L</span><span class="sxs-lookup"><span data-stu-id="3bc5e-400">/L</span></span>
<span data-ttu-id="3bc5e-401">Określa listę operację. dane nie zostaną skopiowane.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="3bc5e-402">Narzędzie AzCopy zinterpretuje przy użyciu tej opcji jako symulacji uruchamiania wiersza polecenia, bez stosowania tej opcji/l i liczba ile obiekty zostaną skopiowane, można określić opcję /V w tym samym czasie, aby sprawdzić, które obiekty zostaną skopiowane pełnego dziennika.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-402">AzCopy will interpret the using of this option as a simulation for running the command line without this option /L and count how many objects will be copied, you can specify option /V at the same time to check which objects will be copied in the verbose log.</span></span>

<span data-ttu-id="3bc5e-403">Zachowanie tej opcji również jest określana przez lokalizację źródła danych i obecność cyklicznego opcji/s i pliku wzorca w trybie /Pattern.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-403">The behavior of this option is also determined by the location of the source data and the presence of the recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="3bc5e-404">Narzędzie AzCopy musi mieć uprawnienie listy i odczytu tej lokalizacji źródła przy użyciu tej opcji.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="3bc5e-405">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="3bc5e-406">/ MT</span><span class="sxs-lookup"><span data-stu-id="3bc5e-406">/MT</span></span>
<span data-ttu-id="3bc5e-407">Ustawia czas ostatniej modyfikacji pobrany plik na taki sam jak źródłowego obiektu blob lub pliku.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-407">Sets the downloaded file's last-modified time to be the same as the source blob or file's.</span></span>

<span data-ttu-id="3bc5e-408">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="3bc5e-409">/XN</span><span class="sxs-lookup"><span data-stu-id="3bc5e-409">/XN</span></span>
<span data-ttu-id="3bc5e-410">Wyklucza nowszej zasobów źródła.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-410">Excludes a newer source resource.</span></span> <span data-ttu-id="3bc5e-411">Zasób nie zostaną skopiowane, jeśli godzina ostatniej modyfikacji źródła jest taka sama lub nowsza niż docelowy.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-411">The resource will not be copied if the last modified time of the source is the same or newer than destination.</span></span>

<span data-ttu-id="3bc5e-412">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="3bc5e-413">/XO</span><span class="sxs-lookup"><span data-stu-id="3bc5e-413">/XO</span></span>
<span data-ttu-id="3bc5e-414">Wyklucza starszych zasobów źródła.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-414">Excludes an older source resource.</span></span> <span data-ttu-id="3bc5e-415">Zasób nie zostaną skopiowane, jeśli godzina ostatniej modyfikacji źródła jest taka sama lub starsza niż docelowy.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-415">The resource will not be copied if the last modified time of the source is the same or older than destination.</span></span>

<span data-ttu-id="3bc5e-416">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="3bc5e-417">/A</span><span class="sxs-lookup"><span data-stu-id="3bc5e-417">/A</span></span>
<span data-ttu-id="3bc5e-418">Wysyła tylko pliki, które mają ustawiony atrybut archiwum.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-418">Uploads only files that have the Archive attribute set.</span></span>

<span data-ttu-id="3bc5e-419">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="3bc5e-420">/ IA: [RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="3bc5e-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="3bc5e-421">Wysyła tylko pliki mające zestawu określonych atrybutów.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-421">Uploads only files that have any of the specified attributes set.</span></span>

<span data-ttu-id="3bc5e-422">Dostępne atrybuty obejmują:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-422">Available attributes include:</span></span>

* <span data-ttu-id="3bc5e-423">R = plików tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="3bc5e-423">R = Read-only files</span></span>
* <span data-ttu-id="3bc5e-424">= Plik gotowy do archiwizacji</span><span class="sxs-lookup"><span data-stu-id="3bc5e-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="3bc5e-425">S = System plików</span><span class="sxs-lookup"><span data-stu-id="3bc5e-425">S = System files</span></span>
* <span data-ttu-id="3bc5e-426">H = ukryte pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-426">H = Hidden files</span></span>
* <span data-ttu-id="3bc5e-427">C = pliki skompresowane</span><span class="sxs-lookup"><span data-stu-id="3bc5e-427">C = Compressed files</span></span>
* <span data-ttu-id="3bc5e-428">N = normalne pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-428">N = Normal files</span></span>
* <span data-ttu-id="3bc5e-429">E = zaszyfrowane pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-429">E = Encrypted files</span></span>
* <span data-ttu-id="3bc5e-430">T = pliki tymczasowe</span><span class="sxs-lookup"><span data-stu-id="3bc5e-430">T = Temporary files</span></span>
* <span data-ttu-id="3bc5e-431">O = plików trybu Offline</span><span class="sxs-lookup"><span data-stu-id="3bc5e-431">O = Offline files</span></span>
* <span data-ttu-id="3bc5e-432">I = indeksowane inne niż pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-432">I = Non-indexed files</span></span>

<span data-ttu-id="3bc5e-433">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="3bc5e-434">/ XA: [RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="3bc5e-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="3bc5e-435">Umożliwia wykluczenie plików, które nie ma żadnej z zestaw określonych atrybutów.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-435">Excludes files that have any of the specified attributes set.</span></span>

<span data-ttu-id="3bc5e-436">Dostępne atrybuty obejmują:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-436">Available attributes include:</span></span>

* <span data-ttu-id="3bc5e-437">R = plików tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="3bc5e-437">R = Read-only files</span></span>
* <span data-ttu-id="3bc5e-438">= Plik gotowy do archiwizacji</span><span class="sxs-lookup"><span data-stu-id="3bc5e-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="3bc5e-439">S = System plików</span><span class="sxs-lookup"><span data-stu-id="3bc5e-439">S = System files</span></span>
* <span data-ttu-id="3bc5e-440">H = ukryte pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-440">H = Hidden files</span></span>
* <span data-ttu-id="3bc5e-441">C = pliki skompresowane</span><span class="sxs-lookup"><span data-stu-id="3bc5e-441">C = Compressed files</span></span>
* <span data-ttu-id="3bc5e-442">N = normalne pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-442">N = Normal files</span></span>
* <span data-ttu-id="3bc5e-443">E = zaszyfrowane pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-443">E = Encrypted files</span></span>
* <span data-ttu-id="3bc5e-444">T = pliki tymczasowe</span><span class="sxs-lookup"><span data-stu-id="3bc5e-444">T = Temporary files</span></span>
* <span data-ttu-id="3bc5e-445">O = plików trybu Offline</span><span class="sxs-lookup"><span data-stu-id="3bc5e-445">O = Offline files</span></span>
* <span data-ttu-id="3bc5e-446">I = indeksowane inne niż pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-446">I = Non-indexed files</span></span>

<span data-ttu-id="3bc5e-447">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="3bc5e-448">/ Ogranicznik: "ogranicznika"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="3bc5e-449">Wskazuje znak ogranicznika używany do ograniczania katalogów wirtualnych w nazwie obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-449">Indicates the delimiter character used to delimit virtual directories in a blob name.</span></span>

<span data-ttu-id="3bc5e-450">Domyślnie używa narzędzia AzCopy / jako znak ogranicznika.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-450">By default, AzCopy uses / as the delimiter character.</span></span> <span data-ttu-id="3bc5e-451">AzCopy obsługuje jednak przy użyciu znaków wspólnych (takich jak @, # lub %) jako ogranicznik.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="3bc5e-452">Jeśli potrzebujesz zawiera jeden z tych znaków specjalnych w wierszu polecenia, należy wpisać nazwę pliku z cudzysłowami podwójnymi.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-452">If you need to include one of these special characters on the command line, enclose the file name with double quotes.</span></span>

<span data-ttu-id="3bc5e-453">Ta opcja ma zastosowanie tylko do pobrania obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="3bc5e-454">**Dotyczy:** obiektów blob</span><span class="sxs-lookup"><span data-stu-id="3bc5e-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="3bc5e-455">/ NC: "numer--równoczesnych operacji"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="3bc5e-456">Określa liczbę jednoczesnych operacji.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-456">Specifies the number of concurrent operations.</span></span>

<span data-ttu-id="3bc5e-457">Narzędzie AzCopy domyślnie uruchamia określonej liczby jednoczesnych operacji w celu zwiększenia przepływności transferu danych.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-457">AzCopy by default starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="3bc5e-458">Należy pamiętać, że dużą liczbą jednoczesnych operacji w środowisku niskiej przepustowości może przeciąży połączenie sieciowe i zapobiec pełni ukończenie operacji.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm the network connection and prevent the operations from fully completing.</span></span> <span data-ttu-id="3bc5e-459">Ograniczenie przepustowości jednoczesnych operacji oparte na rzeczywiste dostępnej przepustowości sieci.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="3bc5e-460">Górny limit liczby jednoczesnych operacji wynosi 512.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-460">The upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="3bc5e-461">**Dotyczy:** obiektów blob, plików, tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="3bc5e-462">/ Źródłowa: "Blob" | "Tabela"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="3bc5e-463">Określa, że `source` zasób jest dostępny w środowisku programistycznym lokalne uruchamianie w emulatorze magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-463">Specifies that the `source` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="3bc5e-464">**Dotyczy:** obiektów blob, tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="3bc5e-465">/ DestType: "Blob" | "Tabela"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="3bc5e-466">Określa, że `destination` zasób jest dostępny w środowisku programistycznym lokalne uruchamianie w emulatorze magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-466">Specifies that the `destination` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="3bc5e-467">**Dotyczy:** obiektów blob, tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="3bc5e-468">/ PKRS: "key1 klucz&#2; klucz&#3;..."</span><span class="sxs-lookup"><span data-stu-id="3bc5e-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="3bc5e-469">Dzieli zakresem kluczy partycji umożliwia eksportowanie danych z tabeli równolegle, co przyspiesza operacji eksportowania.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-469">Splits the partition key range to enable exporting table data in parallel, which increases the speed of the export operation.</span></span>

<span data-ttu-id="3bc5e-470">Jeśli ta opcja nie jest określona, następnie AzCopy używa pojedynczego wątku do wyeksportowania jednostek tabeli.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-470">If this option is not specified, then AzCopy uses a single thread to export table entities.</span></span> <span data-ttu-id="3bc5e-471">Na przykład, jeśli użytkownik określi /PKRS: "aa #bb", a następnie AzCopy uruchamia trzy jednoczesnych operacji.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-471">For example, if the user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="3bc5e-472">Każda operacja eksportuje jednego z trzech zakresów klucza partycji, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="3bc5e-473">[pierwszej partycji klucza, aa)</span><span class="sxs-lookup"><span data-stu-id="3bc5e-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="3bc5e-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="3bc5e-474">[aa, bb)</span></span>

  <span data-ttu-id="3bc5e-475">[bb, ostatnie partycji klucza]</span><span class="sxs-lookup"><span data-stu-id="3bc5e-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="3bc5e-476">**Dotyczy:** tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="3bc5e-477">/ SplitSize: "rozmiar pliku"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="3bc5e-478">Określa wyeksportowany plik podzielić rozmiar w MB, minimalnym dozwolona wartość to 32.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-478">Specifies the exported file split size in MB, the minimal value allowed is 32.</span></span>

<span data-ttu-id="3bc5e-479">Jeśli ta opcja nie jest określona, narzędzie AzCopy będzie eksportować dane w tabeli do pojedynczego pliku.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-479">If this option is not specified, AzCopy will export table data to single file.</span></span>

<span data-ttu-id="3bc5e-480">Jeśli dane w tabeli są eksportowane do obiektu blob, a rozmiar wyeksportowany plik osiągnie limit 200 GB rozmiar obiektu blob, następnie AzCopy podzieli wyeksportowany plik, nawet jeśli ta opcja nie jest określona.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-480">If the table data is exported to a blob, and the exported file size reaches the 200 GB limit for blob size, then AzCopy will split the exported file, even if this option is not specified.</span></span>

<span data-ttu-id="3bc5e-481">**Dotyczy:** tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="3bc5e-482">/ EntityOperation: "InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="3bc5e-483">Określa zachowanie importu danych tabeli.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-483">Specifies the table data import behavior.</span></span>

* <span data-ttu-id="3bc5e-484">InsertOrSkip - pomija istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="3bc5e-485">InsertOrMerge - scala istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="3bc5e-486">InsertOrReplace - zastępuje istniejącej jednostki lub wstawia nową jednostkę, jeśli nie istnieje w tabeli.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="3bc5e-487">**Dotyczy:** tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="3bc5e-488">/ Manifest: "w pliku manifestu"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="3bc5e-489">Określa plik manifestu dla tabeli eksportowania i importowania operacji.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-489">Specifies the manifest file for the table export and import operation.</span></span>

<span data-ttu-id="3bc5e-490">Ta opcja jest opcjonalny podczas operacji eksportowania, AzCopy wygeneruje plik manifestu z wstępnie zdefiniowanej nazwy, jeśli ta opcja nie jest określona.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-490">This option is optional during the export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="3bc5e-491">Ta opcja jest wymagana podczas operacji importowania do lokalizowania plików danych.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-491">This option is required during the import operation for locating the data files.</span></span>

<span data-ttu-id="3bc5e-492">**Dotyczy:** tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="3bc5e-493">/ SyncCopy</span><span class="sxs-lookup"><span data-stu-id="3bc5e-493">/SyncCopy</span></span>
<span data-ttu-id="3bc5e-494">Wskazuje, czy synchronicznie kopiowania obiektów blob lub plików między dwoma punktami końcowymi usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-494">Indicates whether to synchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="3bc5e-495">Narzędzie AzCopy domyślnie używa kopii asynchronicznych po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="3bc5e-496">Wybierz tę opcję w celu wykonania kopii synchroniczne, który pobiera obiektów blob lub pliki do pamięci lokalnej i przekazuje je do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-496">Specify this option to perform a synchronous copy, which downloads blobs or files to local memory and then uploads them to Azure Storage.</span></span>

<span data-ttu-id="3bc5e-497">Tej opcji można użyć podczas kopiowania plików w magazynie obiektów Blob, Magazyn plików, lub z magazynu obiektów Blob do przechowywania plików lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage to File storage or vice versa.</span></span>

<span data-ttu-id="3bc5e-498">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="3bc5e-499">/ SetContentType: "content-type"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="3bc5e-500">Określa typ zawartości MIME docelowym obiektów blob lub plików.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-500">Specifies the MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="3bc5e-501">Domyślnie narzędzie AzCopy ustawia typ zawartości dla obiekt blob lub pliku application/octet-stream.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-501">AzCopy sets the content type for a blob or file to application/octet-stream by default.</span></span> <span data-ttu-id="3bc5e-502">Typ zawartości dla wszystkich obiektów blob lub plików można ustawić jawnie określając wartość dla tej opcji.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-502">You can set the content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="3bc5e-503">Jeśli zostanie określona opcja bez wartości, AzCopy zostanie ustawiony, każdy obiekt blob lub typu zawartości pliku, zgodnie z jego rozszerzenie pliku.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-503">If you specify this option without a value, then AzCopy will set each blob or file's content type according to its file extension.</span></span>

<span data-ttu-id="3bc5e-504">**Dotyczy:** obiektów blob, pliki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="3bc5e-505">/ PayloadFormat: "JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="3bc5e-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="3bc5e-506">Określa format pliku wyeksportowanych danych tabeli.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-506">Specifies the format of the table exported data file.</span></span>

<span data-ttu-id="3bc5e-507">Jeśli ta opcja nie jest określona, domyślnie AzCopy eksportuje plik danych tabeli w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="3bc5e-508">**Dotyczy:** tabel</span><span class="sxs-lookup"><span data-stu-id="3bc5e-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="3bc5e-509">Znane problemy i najlepsze rozwiązania</span><span class="sxs-lookup"><span data-stu-id="3bc5e-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="3bc5e-510">Limit równoczesnych zapisów podczas kopiowania danych</span><span class="sxs-lookup"><span data-stu-id="3bc5e-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="3bc5e-511">Podczas kopiowania obiektów blob lub pliki z narzędzia AzCopy, należy pamiętać, że inna aplikacja może modyfikować danych podczas kopiowania go.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="3bc5e-512">Jeśli to możliwe upewnij się, że dane, które są kopiowane nie jest modyfikowana podczas operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-512">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="3bc5e-513">Na przykład podczas kopiowania wirtualnego dysku twardego skojarzonego z maszyny wirtualnej platformy Azure, upewnij się, że żadne inne aplikacje są obecnie zapisywania wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="3bc5e-514">Dobrym sposobem na to jest dzierżawa zasobów do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-514">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="3bc5e-515">Alternatywnie można najpierw Utwórz migawkę wirtualnego dysku twardego, a następnie skopiuj migawki.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-515">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="3bc5e-516">Jeśli nie można zapobiec inne aplikacje, zapisywania do obiektów blob lub plików, gdy są kopiowane, należy pamiętać, że w czasie, który kończy zadanie, kopiowanych zasobów może nie masz już pełna parzystości z zasobami źródła.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-516">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="3bc5e-517">Uruchom jedno wystąpienie AzCopy na jednej maszynie.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="3bc5e-518">Narzędzie AzCopy zaprojektowano w celu zmaksymalizowania wykorzystania zasobu maszyny w celu przyspieszenia transferu danych, zaleca się uruchomić tylko jedno wystąpienie AzCopy na jednej maszynie i określ opcję `/NC` Jeśli potrzebujesz więcej jednoczesnych operacji.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-518">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="3bc5e-519">Aby uzyskać więcej informacji, wpisz `AzCopy /?:NC` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-519">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="3bc5e-520">Włącz algorytmów MD5 FIPS dla narzędzia AzCopy podczas możesz "Użyj FIPS algorytmów szyfrowania, tworzenia skrótu i podpisywania".</span><span class="sxs-lookup"><span data-stu-id="3bc5e-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="3bc5e-521">AzCopy domyślnie używana implementacja .NET MD5 do obliczenia MD5 podczas kopiowania obiektów, ale istnieją pewne wymagania dotyczące zabezpieczeń, które AzCopy jest potrzebny do Włącz ustawienie MD5, zgodne ze standardem FIPS.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-521">AzCopy by default uses .NET MD5 implementation to calculate the MD5 when copying objects, but there are some security requirements that need AzCopy to enable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="3bc5e-522">Można utworzyć pliku app.config `AzCopy.exe.config` z właściwością `AzureStorageUseV1MD5` i umieszcza je Zarezerwuj z AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="3bc5e-523">Dla właściwości "AzureStorageUseV1MD5" • True — wartość domyślna to narzędzie AzCopy użyje implementacji .NET MD5.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-523">For property "AzureStorageUseV1MD5" • True - The default value, AzCopy will use .NET MD5 implementation.</span></span>
<span data-ttu-id="3bc5e-524">• False — AzCopy będzie używać algorytmu MD5 zgodnego ze standardem FIPS.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-524">• False – AzCopy will use FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="3bc5e-525">Należy pamiętać, że zgodnych algorytmów FIPS jest domyślnie wyłączony na komputerze z systemem Windows można wpisać secpol.msc w oknie Uruchamianie i sprawdzić tego przełącznika na ustawienia zabezpieczeń -> Zabezpieczenia -> Zasady lokalne Opcje -> Kryptografia systemu: Użyj zgodnych algorytmów FIPS dla celów szyfrowania, mieszania i podpisywania.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bc5e-526">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3bc5e-526">Next steps</span></span>
<span data-ttu-id="3bc5e-527">Aby uzyskać więcej informacji na temat usługi Azure Storage i narzędzia AzCopy można znaleźć w następujących zasobach.</span><span class="sxs-lookup"><span data-stu-id="3bc5e-527">For more information about Azure Storage and AzCopy, refer to the following resources.</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="3bc5e-528">Dokumentacja magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="3bc5e-529">Wprowadzenie do usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3bc5e-529">Introduction to Azure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="3bc5e-530">Jak używać magazynu obiektów Blob w .NET</span><span class="sxs-lookup"><span data-stu-id="3bc5e-530">How to use Blob storage from .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="3bc5e-531">Jak używać magazynu plików w .NET</span><span class="sxs-lookup"><span data-stu-id="3bc5e-531">How to use File storage from .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="3bc5e-532">Jak używać magazynu tabel w .NET</span><span class="sxs-lookup"><span data-stu-id="3bc5e-532">How to use Table storage from .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="3bc5e-533">Sposobu tworzenia, zarządzania i usuwania konta magazynu</span><span class="sxs-lookup"><span data-stu-id="3bc5e-533">How to create, manage, or delete a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="3bc5e-534">Transfer danych za pomocą narzędzia AzCopy w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="3bc5e-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="3bc5e-535">Wpisy blogu magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="3bc5e-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="3bc5e-536">Wprowadzenie Podgląd Biblioteka przepływu danych usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3bc5e-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="3bc5e-537">AzCopy: Wprowadzenie do kopiowania synchroniczne i dostosowane typ zawartości</span><span class="sxs-lookup"><span data-stu-id="3bc5e-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="3bc5e-538">Narzędzie AzCopy: Announcing ogólne dostępności 3.0 AzCopy oraz wersji zapoznawczej AzCopy 4.0 z tabeli i plik pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="3bc5e-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="3bc5e-539">Narzędzie AzCopy: Zoptymalizowana pod kątem scenariuszy kopii na dużą skalę</span><span class="sxs-lookup"><span data-stu-id="3bc5e-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="3bc5e-540">AzCopy: Obsługa dostęp do odczytu magazynu geograficznie nadmiarowego</span><span class="sxs-lookup"><span data-stu-id="3bc5e-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="3bc5e-541">Narzędzie AzCopy: Transfer danych za pomocą jej ponownie uruchomić tryb i tokenu sygnatury dostępu Współdzielonego</span><span class="sxs-lookup"><span data-stu-id="3bc5e-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="3bc5e-542">Narzędzia AzCopy: Blob kopiowania między konta przy użyciu</span><span class="sxs-lookup"><span data-stu-id="3bc5e-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="3bc5e-543">Narzędzie AzCopy: Przekazywanie pobieranie plików dla obiektów blob Azure</span><span class="sxs-lookup"><span data-stu-id="3bc5e-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

