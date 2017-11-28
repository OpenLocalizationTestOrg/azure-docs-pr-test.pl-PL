---
title: "Kopiowanie lub przenoszenie danych do magazynu Azure z narzędzia AzCopy w systemie Linux | Dokumentacja firmy Microsoft"
description: "W systemie AzCopy Linux narzędzia do przenoszenia lub kopiowania danych do lub z obiektu blob i zawartości pliku. Kopiowanie danych do magazynu Azure z lokalnych plików lub kopiowania danych w ramach urządzeń magazynujących lub między kontami magazynu. Łatwo przeprowadzić migrację danych do usługi Azure Storage."
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
ms.openlocfilehash: 441227d84b9c1ec721ae36fdc423ba797654f128
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="30368-105">Transfer danych za pomocą narzędzia AzCopy w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="30368-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="30368-106">AzCopy w systemie Linux to narzędzie wiersza polecenia przeznaczone do kopiowania danych z magazynu obiektów Blob Microsoft Azure i plików przy użyciu prostych poleceń z optymalną wydajnością.</span><span class="sxs-lookup"><span data-stu-id="30368-106">AzCopy on Linux is a command-line utility designed for copying data to and from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="30368-107">Można skopiować danych z jednego obiektu do drugiego, w ramach konta magazynu lub między kontami magazynu.</span><span class="sxs-lookup"><span data-stu-id="30368-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="30368-108">Istnieją dwie wersje programu AzCopy, który można pobrać.</span><span class="sxs-lookup"><span data-stu-id="30368-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="30368-109">W systemie Linux azcopy jest z platformy .NET Core Framework, który jest przeznaczony dla platformy Linux oferty styl POSIX opcje wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="30368-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="30368-110">[Narzędzie AzCopy w systemie Windows](../storage-use-azcopy.md) jest oparty na platformie .NET Framework i oferuje opcje wiersza polecenia Styl systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="30368-110">[AzCopy on Windows](../storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="30368-111">W tym artykule omówiono AzCopy w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="30368-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="30368-112">Pobierz i zainstaluj narzędzie AzCopy</span><span class="sxs-lookup"><span data-stu-id="30368-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="30368-113">Instalacja w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="30368-113">Installation on Linux</span></span>

<span data-ttu-id="30368-114">Narzędzie AzCopy w systemie Linux wymaga platformy .NET Core framework na platformie.</span><span class="sxs-lookup"><span data-stu-id="30368-114">AzCopy on Linux requires .NET Core framework on the platform.</span></span> <span data-ttu-id="30368-115">Zapoznaj się z instrukcjami instalacji na [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) strony.</span><span class="sxs-lookup"><span data-stu-id="30368-115">See the installation instructions on the [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="30368-116">Na przykład załóżmy Zainstaluj oprogramowanie .NET Core na Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="30368-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="30368-117">Najnowszy przewodnik instalacji można znaleźć [.NET Core w systemie Linux](https://www.microsoft.com/net/core#linuxubuntu) strona instalacji.</span><span class="sxs-lookup"><span data-stu-id="30368-117">For the latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="30368-118">Po zainstalowaniu platformy .NET Core, Pobierz i zainstaluj narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="30368-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="30368-119">Po zainstalowaniu narzędzia AzCopy w systemie Linux, możesz usunąć wyodrębnione pliki.</span><span class="sxs-lookup"><span data-stu-id="30368-119">You can remove the extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="30368-120">Alternatywnie, jeśli nie masz uprawnień administratora, można również uruchomić za pomocą skryptu powłoki "azcopy" w folderze wyodrębnione narzędzie AzCopy.</span><span class="sxs-lookup"><span data-stu-id="30368-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using the shell script 'azcopy' in the extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="30368-121">Alternatywne instalacji na Ubuntu</span><span class="sxs-lookup"><span data-stu-id="30368-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="30368-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="30368-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="30368-123">Dodawanie źródła stanie dla platformy .net Core:</span><span class="sxs-lookup"><span data-stu-id="30368-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="30368-124">Dodaj stanie źródło repozytorium produktu Linux firmy Microsoft i zainstalować narzędzia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="30368-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="30368-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="30368-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="30368-126">Dodawanie źródła stanie dla platformy .net Core:</span><span class="sxs-lookup"><span data-stu-id="30368-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="30368-127">Dodaj stanie źródło repozytorium produktu Linux firmy Microsoft i zainstalować narzędzia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="30368-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="30368-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="30368-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="30368-129">Dodawanie źródła stanie dla platformy .net Core:</span><span class="sxs-lookup"><span data-stu-id="30368-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="30368-130">Dodaj stanie źródło repozytorium produktu Linux firmy Microsoft i zainstalować narzędzia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="30368-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="30368-131">Pisanie pierwszego polecenia AzCopy</span><span class="sxs-lookup"><span data-stu-id="30368-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="30368-132">Podstawowa składnia polecenia AzCopy jest:</span><span class="sxs-lookup"><span data-stu-id="30368-132">The basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="30368-133">W poniższych przykładach pokazano różne scenariusze kopiowania danych do i z obiektach blob Microsoft Azure i plików.</span><span class="sxs-lookup"><span data-stu-id="30368-133">The following examples demonstrate various scenarios for copying data to and from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="30368-134">Zapoznaj się `azcopy --help` menu, aby uzyskać szczegółowy opis parametry używane w każdej próbce.</span><span class="sxs-lookup"><span data-stu-id="30368-134">Refer to the `azcopy --help` menu for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="30368-135">Obiekt blob: Pobierz</span><span class="sxs-lookup"><span data-stu-id="30368-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="30368-136">Pobieranie pojedynczego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="30368-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="30368-137">Jeśli folder `/mnt/myfiles` nie istnieje, narzędzie AzCopy tworzy go i pobiera `abc.txt ` do nowego folderu.</span><span class="sxs-lookup"><span data-stu-id="30368-137">If the folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="30368-138">Pobieranie pojedynczego obiektu blob z regionu pomocniczego</span><span class="sxs-lookup"><span data-stu-id="30368-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="30368-139">Należy pamiętać, że użytkownik musi mieć dostęp do odczytu magazynu geograficznie nadmiarowego włączone.</span><span class="sxs-lookup"><span data-stu-id="30368-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="30368-140">Pobierz wszystkie obiekty BLOB</span><span class="sxs-lookup"><span data-stu-id="30368-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="30368-141">Przyjęto założenie, że następujące obiekty BLOB znajdują się w określonym kontenerze:</span><span class="sxs-lookup"><span data-stu-id="30368-141">Assume the following blobs reside in the specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="30368-142">Po wykonaniu operacji pobierania katalogu `/mnt/myfiles` zawiera następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="30368-142">After the download operation, the directory `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="30368-143">Jeśli nie zostanie określona opcja `--recursive`, nie obiektu blob zostaną pobrane.</span><span class="sxs-lookup"><span data-stu-id="30368-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="30368-144">Pobieranie obiektów blob z określonego prefiksu</span><span class="sxs-lookup"><span data-stu-id="30368-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="30368-145">Załóżmy, że następujące obiekty BLOB znajdują się w określonym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="30368-145">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="30368-146">Wszystkie obiekty BLOB rozpoczynający się od prefiksu `a` zostaną pobrane.</span><span class="sxs-lookup"><span data-stu-id="30368-146">All blobs beginning with the prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="30368-147">Po wykonaniu operacji pobierania folderu `/mnt/myfiles` zawiera następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="30368-147">After the download operation, the folder `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="30368-148">Prefiks ma zastosowanie do katalogu wirtualnego, który stanowi pierwsza część nazwy obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="30368-148">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="30368-149">W powyższym przykładzie katalogu wirtualnego jest niezgodny określony prefiks tak blob nie zostanie pobrana.</span><span class="sxs-lookup"><span data-stu-id="30368-149">In the example shown above, the virtual directory does not match the specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="30368-150">Ponadto jeśli opcja `--recursive` nie zostanie określony, narzędzie AzCopy nie pobiera wszystkie obiekty BLOB.</span><span class="sxs-lookup"><span data-stu-id="30368-150">In addition, if the option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="30368-151">Ustawianie czasu ostatniej modyfikacji plików wyeksportowane taka sama jak obiekty BLOB źródła</span><span class="sxs-lookup"><span data-stu-id="30368-151">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="30368-152">Można również wykluczyć obiekty BLOB z operacji pobierania na podstawie ich czasu ostatniej modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="30368-152">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="30368-153">Na przykład, jeśli chcesz wykluczyć obiekty BLOB, którego ostatniej modyfikacji jest taką samą lub nowszą niż plik docelowy Dodaj `--exclude-newer` opcji:</span><span class="sxs-lookup"><span data-stu-id="30368-153">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="30368-154">Lub jeśli chcesz wykluczyć obiekty BLOB, którego ostatniej modyfikacji tego samego lub starsze niż plik docelowy Dodaj `--exclude-older` opcji:</span><span class="sxs-lookup"><span data-stu-id="30368-154">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="30368-155">Obiekt blob: Przekaż</span><span class="sxs-lookup"><span data-stu-id="30368-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="30368-156">Przekaż pojedynczy plik</span><span class="sxs-lookup"><span data-stu-id="30368-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="30368-157">Jeśli docelowy określony kontener nie istnieje, AzCopy tworzy go i przekazuje plik do niego.</span><span class="sxs-lookup"><span data-stu-id="30368-157">If the specified destination container does not exist, AzCopy creates it and uploads the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="30368-158">Przekaż pojedynczy plik do katalogu wirtualnego</span><span class="sxs-lookup"><span data-stu-id="30368-158">Upload single file to virtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="30368-159">Jeśli określony katalog wirtualny nie istnieje, narzędzie AzCopy przekazywania pliku, aby uwzględnić w nazwie obiektu blob katalogu wirtualnego (*np.*, `vd/abc.txt` w powyższym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="30368-159">If the specified virtual directory does not exist, AzCopy uploads the file to include the virtual directory in the blob name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="30368-160">Przekaż wszystkie pliki</span><span class="sxs-lookup"><span data-stu-id="30368-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="30368-161">Określenie opcji `--recursive` przekazuje zawartość określonego katalogu rekursywnie magazynu obiektów Blob, co oznacza, jak również przekazać wszystkie podfoldery i pliki.</span><span class="sxs-lookup"><span data-stu-id="30368-161">Specifying option `--recursive` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="30368-162">Na przykład załóżmy następujące pliki znajdują się w folderze `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="30368-162">For instance, assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="30368-163">Po wykonaniu operacji przekazywania kontener zawiera następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="30368-163">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="30368-164">Gdy opcja `--recursive` nie zostanie określony, są przekazywane tylko trzy następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="30368-164">When the option `--recursive` is not specified, only the following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="30368-165">Przekazywanie plików zgodnych z określonym wzorcem</span><span class="sxs-lookup"><span data-stu-id="30368-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="30368-166">Załóżmy następujące pliki znajdują się w folderze `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="30368-166">Assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="30368-167">Po wykonaniu operacji przekazywania kontener zawiera następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="30368-167">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="30368-168">Gdy opcja `--recursive` nie zostanie określony, narzędzie AzCopy pomija pliki, które są w katalogach podrzędnych:</span><span class="sxs-lookup"><span data-stu-id="30368-168">When the option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="30368-169">Określ typ zawartości MIME docelowego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="30368-169">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="30368-170">Domyślnie narzędzie AzCopy ustawia typ zawartości do docelowego obiektu blob `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="30368-170">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="30368-171">Jednak jawnie określić typ zawartości przy użyciu opcji `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="30368-171">However, you can explicitly specify the content type via the option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="30368-172">Ta składnia ustawia typ zawartości dla wszystkich obiektów blob w operacji przekazywania.</span><span class="sxs-lookup"><span data-stu-id="30368-172">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="30368-173">Jeśli opcja `--set-content-type` jest określony bez wartości, a następnie ustawia AzCopy każdy obiekt blob lub typ zawartości pliku, zgodnie z jego rozszerzenie pliku.</span><span class="sxs-lookup"><span data-stu-id="30368-173">If the option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according to its file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="30368-174">Obiekt blob: kopiowania</span><span class="sxs-lookup"><span data-stu-id="30368-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="30368-175">Skopiuj pojedynczego obiektu blob w ramach konta magazynu</span><span class="sxs-lookup"><span data-stu-id="30368-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="30368-176">Podczas kopiowania obiektu blob bez — opcja synchronizacji kopii [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="30368-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="30368-177">Skopiuj pojedynczego obiektu blob na kontach magazynu</span><span class="sxs-lookup"><span data-stu-id="30368-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="30368-178">Podczas kopiowania obiektu blob bez — opcja synchronizacji kopii [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="30368-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="30368-179">Skopiuj pojedynczego obiektu blob z regionu pomocniczego do regionu podstawowego</span><span class="sxs-lookup"><span data-stu-id="30368-179">Copy single blob from secondary region to primary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="30368-180">Należy pamiętać, że użytkownik musi mieć dostęp do odczytu magazynu geograficznie nadmiarowego włączone.</span><span class="sxs-lookup"><span data-stu-id="30368-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="30368-181">Skopiuj pojedynczego obiektu blob i jego migawek wielu kont magazynu</span><span class="sxs-lookup"><span data-stu-id="30368-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="30368-182">Po wykonaniu operacji kopiowania kontenera docelowego obejmuje obiektu blob i jego migawek.</span><span class="sxs-lookup"><span data-stu-id="30368-182">After the copy operation, the target container includes the blob and its snapshots.</span></span> <span data-ttu-id="30368-183">Kontener zawiera jego migawki i następujących obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="30368-183">The container includes the following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="30368-184">Synchronicznie skopiować wielu kont magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="30368-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="30368-185">Narzędzie AzCopy domyślnie kopiuje dane między dwoma punktami końcowymi magazynu asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="30368-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="30368-186">W związku z tym jest kopiowana uruchamia operację kopiowania w tle przy użyciu pojemności nieużywanej przepustowości ma umowy dotyczącej poziomu usług pod względem sposobu szybkiego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="30368-186">Therefore, the copy operation runs in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="30368-187">`--sync-copy` Opcja zapewnia, że operacji kopiowania pobiera spójne szybkości.</span><span class="sxs-lookup"><span data-stu-id="30368-187">The `--sync-copy` option ensures that the copy operation gets consistent speed.</span></span> <span data-ttu-id="30368-188">Narzędzie AzCopy wykonuje synchroniczne kopiowania pobieranie obiektów blob można skopiować z określonego źródła do pamięci lokalnej, a następnie przekazywanie ich do miejsce docelowe magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="30368-188">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="30368-189">`--sync-copy`może generować dodatkowe wyjście koszt w porównaniu do kopiowania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="30368-189">`--sync-copy` might generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="30368-190">Zalecanym podejściem jest użycie tej opcji w maszynie Wirtualnej platformy Azure, który znajduje się w tym samym regionie co konta magazynu źródłowego, aby uniknąć kosztów wyjście.</span><span class="sxs-lookup"><span data-stu-id="30368-190">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="30368-191">Plik: Pobierz</span><span class="sxs-lookup"><span data-stu-id="30368-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="30368-192">Pobierz pojedynczy plik</span><span class="sxs-lookup"><span data-stu-id="30368-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="30368-193">Jeśli określone źródło jest udział plików na platformę Azure, a następnie podaj nazwę pliku dokładną (*np.* `abc.txt`) do pobrania pojedynczy plik, lub określ opcję `--recursive` Aby pobrać wszystkie pliki w udziale rekursywnie.</span><span class="sxs-lookup"><span data-stu-id="30368-193">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `--recursive` to download all files in the share recursively.</span></span> <span data-ttu-id="30368-194">Podjęto próbę Określ wzorzec pliku i opcji `--recursive` razem powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="30368-194">Attempting to specify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="30368-195">Pobierz wszystkie pliki</span><span class="sxs-lookup"><span data-stu-id="30368-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="30368-196">Należy pamiętać, że puste foldery nie zostaną pobrane.</span><span class="sxs-lookup"><span data-stu-id="30368-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="30368-197">Plik: Przekaż</span><span class="sxs-lookup"><span data-stu-id="30368-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="30368-198">Przekaż pojedynczy plik</span><span class="sxs-lookup"><span data-stu-id="30368-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="30368-199">Przekaż wszystkie pliki</span><span class="sxs-lookup"><span data-stu-id="30368-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="30368-200">Należy pamiętać, że wszystkie puste foldery nie zostały przekazane.</span><span class="sxs-lookup"><span data-stu-id="30368-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="30368-201">Przekazywanie plików zgodnych z określonym wzorcem</span><span class="sxs-lookup"><span data-stu-id="30368-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="30368-202">Plik: kopiowania</span><span class="sxs-lookup"><span data-stu-id="30368-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="30368-203">Kopiowanie między udziałami plików</span><span class="sxs-lookup"><span data-stu-id="30368-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="30368-204">Podczas kopiowania plików między udziałami plików [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="30368-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="30368-205">Kopiowanie z udziału plików do obiektu blob</span><span class="sxs-lookup"><span data-stu-id="30368-205">Copy from file share to blob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="30368-206">Podczas kopiowania pliku z udziału plików do obiektów blob, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="30368-206">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="30368-207">Kopiowanie z obiektu blob do udziału plików</span><span class="sxs-lookup"><span data-stu-id="30368-207">Copy from blob to file share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="30368-208">Podczas kopiowania pliku z obiektu blob do udziału plików, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="30368-208">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="30368-209">Synchronicznie kopiować pliki</span><span class="sxs-lookup"><span data-stu-id="30368-209">Synchronously copy files</span></span>
<span data-ttu-id="30368-210">Można określić `--sync-copy` opcję, aby skopiować dane z pliku magazynu do przechowywania plików, z pliku magazynu do magazynu obiektów Blob i z magazynu obiektów Blob do przechowywania plików synchronicznie.</span><span class="sxs-lookup"><span data-stu-id="30368-210">You can specify the `--sync-copy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously.</span></span> <span data-ttu-id="30368-211">Narzędzie AzCopy uruchamia tej operacji pobierania danych źródłowych do pamięci lokalnej, a następnie przekazać go do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="30368-211">AzCopy runs this operation by downloading the source data to local memory, and then uploading it to destination.</span></span> <span data-ttu-id="30368-212">W tym przypadku standardowe wyjście koszt dotyczy.</span><span class="sxs-lookup"><span data-stu-id="30368-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="30368-213">Podczas kopiowania z pliku magazynu do magazynu obiektów Blob, domyślnym typem obiektu blob jest blokowych obiektów blob, użytkownik może określić opcję `/BlobType:page` zmienić typ docelowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="30368-213">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="30368-214">Należy pamiętać, że `--sync-copy` może generować wyjście dodatkowych kosztów porównanie kopii asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="30368-214">Note that `--sync-copy` might generate additional egress cost comparing to asynchronous copy.</span></span> <span data-ttu-id="30368-215">Zalecanym podejściem jest użycie tej opcji w maszynie Wirtualnej platformy Azure, który znajduje się w tym samym regionie co konta magazynu źródłowego, aby uniknąć kosztów wyjście.</span><span class="sxs-lookup"><span data-stu-id="30368-215">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="30368-216">Inne funkcje AzCopy</span><span class="sxs-lookup"><span data-stu-id="30368-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="30368-217">Tylko skopiować dane, które nie istnieje w docelowym</span><span class="sxs-lookup"><span data-stu-id="30368-217">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="30368-218">`--exclude-older` i `--exclude-newer` parametry umożliwiają Wyklucz zasoby starszej lub nowszej źródła zapobiega kopiowaniu odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="30368-218">The `--exclude-older` and `--exclude-newer` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="30368-219">Jeśli chcesz skopiować źródła zasobów, które nie istnieje w docelowym, można określić oba parametry polecenia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="30368-219">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-to-specify-command-line-parameters"></a><span data-ttu-id="30368-220">Aby określić parametry wiersza polecenia przy użyciu pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="30368-220">Use a configuration file to specify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="30368-221">Parametry wiersza polecenia AzCopy można uwzględnić w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="30368-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="30368-222">Narzędzie AzCopy przetwarza parametrów w pliku tak, jakby były one określone w wierszu polecenia wykonywanie bezpośrednich podstawienia z zawartością pliku.</span><span class="sxs-lookup"><span data-stu-id="30368-222">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="30368-223">Załóżmy plik konfiguracji o nazwie `copyoperation`, który zawiera następujące wiersze.</span><span class="sxs-lookup"><span data-stu-id="30368-223">Assume a configuration file named `copyoperation`, that contains the following lines.</span></span> <span data-ttu-id="30368-224">Każdy parametr narzędzia AzCopy można określić w jednym wierszu.</span><span class="sxs-lookup"><span data-stu-id="30368-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="30368-225">lub na oddzielnych wierszach:</span><span class="sxs-lookup"><span data-stu-id="30368-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="30368-226">Narzędzie AzCopy wynik negatywny, jeśli parametr można podzielić na dwa wiersze, jak pokazano poniżej, aby uzyskać `--source-key` parametru:</span><span class="sxs-lookup"><span data-stu-id="30368-226">AzCopy fails if you split the parameter across two lines, as shown here for the `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="30368-227">Określ sygnatury dostępu współdzielonego (SAS)</span><span class="sxs-lookup"><span data-stu-id="30368-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="30368-228">Można również określić sygnatury dostępu Współdzielonego w kontenerze identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="30368-228">You can also specify a SAS on the container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="30368-229">Należy pamiętać, że narzędzie AzCopy aktualnie obsługuje tylko [SAS konta](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="30368-229">Note that AzCopy currently only supports the [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="30368-230">Folder plików dziennika</span><span class="sxs-lookup"><span data-stu-id="30368-230">Journal file folder</span></span>
<span data-ttu-id="30368-231">Zawsze, gdy wydać polecenie do narzędzia AzCopy, sprawdza czy istnieje w pliku dziennika w domyślnym folderze, lub czy istnieje w folderze określonej za pomocą tej opcji.</span><span class="sxs-lookup"><span data-stu-id="30368-231">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="30368-232">Jeśli plik dziennika nie istnieje w każdym miejscu, AzCopy traktuje jako nowe działanie i generuje nowy plik dziennika.</span><span class="sxs-lookup"><span data-stu-id="30368-232">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="30368-233">Jeśli plik dziennika istnieje, narzędzie AzCopy sprawdza, czy wiersz polecenia, który możesz wpisać zgodny wiersz polecenia w pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="30368-233">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="30368-234">Jeśli dwa wiersze poleceń są zgodne, AzCopy wznawia działanie niekompletne.</span><span class="sxs-lookup"><span data-stu-id="30368-234">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="30368-235">Jeśli nie są zgodne, AzCopy monituje użytkownika albo zastąpienie pliku dziennika można uruchomić nowej operacji lub Anuluj bieżącą operację.</span><span class="sxs-lookup"><span data-stu-id="30368-235">If they do not match, AzCopy prompts user to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="30368-236">Jeśli chcesz użyć domyślnej lokalizacji pliku dziennika:</span><span class="sxs-lookup"><span data-stu-id="30368-236">If you want to use the default location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="30368-237">Jeśli pominięto opcję `--resume`, lub określ opcję `--resume` bez ścieżkę do folderu, jak pokazano powyżej, AzCopy tworzy plik dziennika w lokalizacji domyślnej, która jest `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="30368-237">If you omit option `--resume`, or specify option `--resume` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="30368-238">Jeśli istnieje już plik dziennika, AzCopy wznawia działanie na podstawie pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="30368-238">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="30368-239">Jeśli chcesz określić niestandardową lokalizację pliku dziennika:</span><span class="sxs-lookup"><span data-stu-id="30368-239">If you want to specify a custom location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="30368-240">W tym przykładzie powoduje utworzenie pliku dziennika, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="30368-240">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="30368-241">Jeśli istnieje, narzędzie AzCopy wznawia działanie na podstawie pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="30368-241">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="30368-242">Jeśli chcesz wznowić działanie narzędzia AzCopy, powtórz tego samego polecenia.</span><span class="sxs-lookup"><span data-stu-id="30368-242">If you want to resume an AzCopy operation, repeat the same command.</span></span> <span data-ttu-id="30368-243">Narzędzie AzCopy w systemie Linux następnie wyświetli monit o potwierdzenie:</span><span class="sxs-lookup"><span data-stu-id="30368-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at the journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want to resume the operation? Choose Yes to resume, choose No to overwrite the journal to start a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="30368-244">Dzienniki pełne dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="30368-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="30368-245">Określ liczbę jednoczesnych operacji można uruchomić</span><span class="sxs-lookup"><span data-stu-id="30368-245">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="30368-246">Opcja `--parallel-level` określa liczbę jednoczesnych kopii operacji.</span><span class="sxs-lookup"><span data-stu-id="30368-246">Option `--parallel-level` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="30368-247">Domyślnie narzędzie AzCopy uruchamia określonej liczby jednoczesnych operacji w celu zwiększenia przepływności transferu danych.</span><span class="sxs-lookup"><span data-stu-id="30368-247">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="30368-248">Liczba jednoczesnych operacji jest równa osiem razy liczba procesorów masz.</span><span class="sxs-lookup"><span data-stu-id="30368-248">The number of concurrent operations is equal eight times the number of processors you have.</span></span> <span data-ttu-id="30368-249">Jeśli używasz narzędzia AzCopy w niskiej przepustowości sieci, można określić niższą dla — poziom równolegle w celu uniknięcia błąd spowodowany konkurencji zasobów.</span><span class="sxs-lookup"><span data-stu-id="30368-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level to avoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="30368-250">Aby wyświetlić pełną listę parametrów narzędzia AzCopy, zapoznaj się "azcopy--pomocy" menu.</span><span class="sxs-lookup"><span data-stu-id="30368-250">To view the complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="30368-251">Znane problemy i najlepsze rozwiązania</span><span class="sxs-lookup"><span data-stu-id="30368-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-the-system"></a><span data-ttu-id="30368-252">Błąd: Nie znaleziono .NET Core w systemie.</span><span class="sxs-lookup"><span data-stu-id="30368-252">Error: .NET Core is not found in the system.</span></span>
<span data-ttu-id="30368-253">Jeśli wystąpią komunikat o błędzie informujący, że oprogramowanie .NET Core nie jest zainstalowany w systemie, ŚCIEŻKA do pliku binarnego .NET Core `dotnet` może brakować.</span><span class="sxs-lookup"><span data-stu-id="30368-253">If you encounter an error stating that .NET Core is not installed in the system, the PATH to the .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="30368-254">Aby rozwiązać ten problem, należy znaleźć .NET Core pliku binarnego w systemie:</span><span class="sxs-lookup"><span data-stu-id="30368-254">In order to address this issue, find the .NET Core binary in the system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="30368-255">To zwraca ścieżkę do dotnet binarnego.</span><span class="sxs-lookup"><span data-stu-id="30368-255">This returns the path to the dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="30368-256">Teraz Dodaj tę ścieżkę do zmiennej PATH.</span><span class="sxs-lookup"><span data-stu-id="30368-256">Now add this path to the PATH variable.</span></span> <span data-ttu-id="30368-257">Sudo Edytuj secure_path zawiera ścieżkę do dotnet binarne:</span><span class="sxs-lookup"><span data-stu-id="30368-257">For sudo, edit secure_path to contain the path to the dotnet binary:</span></span>
```bash 
sudo visudo
### Append the path found in the preceding example to 'secure_path' variable
```

<span data-ttu-id="30368-258">W tym przykładzie zmienna secure_path odczytuje jako:</span><span class="sxs-lookup"><span data-stu-id="30368-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="30368-259">Dla bieżącego użytkownika należy edytować.bash_profile/.profile do zawiera ścieżkę do binarnego w zmiennej PATH dotnet</span><span class="sxs-lookup"><span data-stu-id="30368-259">For the current user, edit .bash_profile/.profile to include the path to the dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append the path found in the preceding example to 'PATH' variable
```

<span data-ttu-id="30368-260">Sprawdź, czy oprogramowanie .NET Core jest w ŚCIEŻCE:</span><span class="sxs-lookup"><span data-stu-id="30368-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="30368-261">Błąd podczas instalowania narzędzia AzCopy</span><span class="sxs-lookup"><span data-stu-id="30368-261">Error Installing AzCopy</span></span>
<span data-ttu-id="30368-262">Jeśli wystąpią problemy z instalacją AzCopy może zostanie podjęta próba uruchomienia narzędzia AzCopy przy użyciu skryptu bash w wyodrębnionego `azcopy` folderu.</span><span class="sxs-lookup"><span data-stu-id="30368-262">If you encounter issues with AzCopy installation, you may try to run AzCopy using the bash script in the extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="30368-263">Limit równoczesnych zapisów podczas kopiowania danych</span><span class="sxs-lookup"><span data-stu-id="30368-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="30368-264">Podczas kopiowania obiektów blob lub pliki z narzędzia AzCopy, należy pamiętać, że inna aplikacja może modyfikować danych podczas kopiowania go.</span><span class="sxs-lookup"><span data-stu-id="30368-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="30368-265">Jeśli to możliwe upewnij się, że dane, które są kopiowane nie jest modyfikowana podczas operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="30368-265">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="30368-266">Na przykład podczas kopiowania wirtualnego dysku twardego skojarzonego z maszyny wirtualnej platformy Azure, upewnij się, że żadne inne aplikacje są obecnie zapisywania wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="30368-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="30368-267">Dobrym sposobem na to jest dzierżawa zasobów do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="30368-267">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="30368-268">Alternatywnie można najpierw Utwórz migawkę wirtualnego dysku twardego, a następnie skopiuj migawki.</span><span class="sxs-lookup"><span data-stu-id="30368-268">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="30368-269">Jeśli nie można zapobiec inne aplikacje, zapisywania do obiektów blob lub plików, gdy są kopiowane, należy pamiętać, że w czasie, który kończy zadanie, kopiowanych zasobów może nie masz już pełna parzystości z zasobami źródła.</span><span class="sxs-lookup"><span data-stu-id="30368-269">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="30368-270">Uruchom jedno wystąpienie AzCopy na jednej maszynie.</span><span class="sxs-lookup"><span data-stu-id="30368-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="30368-271">Narzędzie AzCopy zaprojektowano w celu zmaksymalizowania wykorzystania zasobu maszyny w celu przyspieszenia transferu danych, zaleca się uruchomić tylko jedno wystąpienie AzCopy na jednej maszynie i określ opcję `--parallel-level` Jeśli potrzebujesz więcej jednoczesnych operacji.</span><span class="sxs-lookup"><span data-stu-id="30368-271">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="30368-272">Aby uzyskać więcej informacji, wpisz `AzCopy --help parallel-level` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="30368-272">For more details, type `AzCopy --help parallel-level` at the command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30368-273">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30368-273">Next steps</span></span>
<span data-ttu-id="30368-274">Aby uzyskać więcej informacji na temat usługi Azure Storage i AzCopy zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="30368-274">For more information about Azure Storage and AzCopy, see the following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="30368-275">Dokumentacja magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="30368-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="30368-276">Wprowadzenie do usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="30368-276">Introduction to Azure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="30368-277">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="30368-277">Create a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="30368-278">Zarządzanie obiektów blob z Eksploratora usługi Storage</span><span class="sxs-lookup"><span data-stu-id="30368-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="30368-279">Za pomocą usługi Azure CLI 2.0 z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="30368-279">Using the Azure CLI 2.0 with Azure Storage</span></span>](../storage-azure-cli.md)
* [<span data-ttu-id="30368-280">Jak używać magazynu obiektów Blob w języku C++</span><span class="sxs-lookup"><span data-stu-id="30368-280">How to use Blob storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="30368-281">Używanie usługi Blob Storage w języku Java</span><span class="sxs-lookup"><span data-stu-id="30368-281">How to use Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="30368-282">Używanie usługi Blob Storage w oprogramowaniu Node.js</span><span class="sxs-lookup"><span data-stu-id="30368-282">How to use Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="30368-283">Używanie usługi Blob Storage w języku Python</span><span class="sxs-lookup"><span data-stu-id="30368-283">How to use Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="30368-284">Wpisy blogu magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="30368-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="30368-285">Anonsowanie AzCopy w wersji zapoznawczej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="30368-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="30368-286">Wprowadzenie Podgląd Biblioteka przepływu danych usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="30368-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="30368-287">AzCopy: Wprowadzenie do kopiowania synchroniczne i dostosowane typ zawartości</span><span class="sxs-lookup"><span data-stu-id="30368-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="30368-288">Narzędzie AzCopy: Announcing ogólne dostępności 3.0 AzCopy oraz wersji zapoznawczej AzCopy 4.0 z tabeli i plik pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="30368-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="30368-289">Narzędzie AzCopy: Zoptymalizowana pod kątem scenariuszy kopii na dużą skalę</span><span class="sxs-lookup"><span data-stu-id="30368-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="30368-290">AzCopy: Obsługa dostęp do odczytu magazynu geograficznie nadmiarowego</span><span class="sxs-lookup"><span data-stu-id="30368-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="30368-291">Narzędzie AzCopy: Transfer danych za pomocą trybu ponownego uruchamiania i tokenu sygnatury dostępu Współdzielonego</span><span class="sxs-lookup"><span data-stu-id="30368-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="30368-292">Narzędzia AzCopy: Blob kopiowania między konta przy użyciu</span><span class="sxs-lookup"><span data-stu-id="30368-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="30368-293">Narzędzie AzCopy: Przekazywanie pobieranie plików dla obiektów blob Azure</span><span class="sxs-lookup"><span data-stu-id="30368-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

