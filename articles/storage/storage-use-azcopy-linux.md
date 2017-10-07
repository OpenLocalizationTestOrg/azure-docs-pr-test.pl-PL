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
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="4fe4f-105">Transfer danych za pomocą narzędzia AzCopy w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="4fe4f-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="4fe4f-106">AzCopy w systemie Linux to narzędzie wiersza polecenia przeznaczone do kopiowania tooand danych z magazynu obiektów Blob Microsoft Azure i plików przy użyciu prostych poleceń z optymalną wydajnością.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-106">AzCopy on Linux is a command-line utility designed for copying data tooand from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="4fe4f-107">Możesz skopiować dane z jednego obiektu tooanother w ramach konta magazynu lub między kontami magazynu.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="4fe4f-108">Istnieją dwie wersje programu AzCopy, który można pobrać.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="4fe4f-109">W systemie Linux azcopy jest z platformy .NET Core Framework, który jest przeznaczony dla platformy Linux oferty styl POSIX opcje wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="4fe4f-110">[Narzędzie AzCopy w systemie Windows](storage-use-azcopy.md) jest oparty na platformie .NET Framework i oferuje opcje wiersza polecenia Styl systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-110">[AzCopy on Windows](storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="4fe4f-111">W tym artykule omówiono AzCopy w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="4fe4f-112">Pobierz i zainstaluj narzędzie AzCopy</span><span class="sxs-lookup"><span data-stu-id="4fe4f-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="4fe4f-113">Instalacja w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="4fe4f-113">Installation on Linux</span></span>

<span data-ttu-id="4fe4f-114">Narzędzie AzCopy w systemie Linux wymaga platformy .NET Core framework na platformie hello.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-114">AzCopy on Linux requires .NET Core framework on hello platform.</span></span> <span data-ttu-id="4fe4f-115">Zobacz instrukcje dotyczące instalacji hello na powitania [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) strony.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-115">See hello installation instructions on hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="4fe4f-116">Na przykład załóżmy Zainstaluj oprogramowanie .NET Core na Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="4fe4f-117">Hello najnowsze Przewodnik instalacji, odwiedź stronę [.NET Core w systemie Linux](https://www.microsoft.com/net/core#linuxubuntu) strona instalacji.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-117">For hello latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="4fe4f-118">Po zainstalowaniu platformy .NET Core, Pobierz i zainstaluj narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="4fe4f-119">Po zainstalowaniu narzędzia AzCopy w systemie Linux, możesz usunąć pliki hello wyodrębnione.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-119">You can remove hello extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="4fe4f-120">Alternatywnie, jeśli nie masz uprawnień administratora, można również uruchomić AzCopy za pomocą skryptu powłoki hello "azcopy" hello wyodrębnionego folderu.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using hello shell script 'azcopy' in hello extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="4fe4f-121">Alternatywne instalacji na Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4fe4f-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="4fe4f-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="4fe4f-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="4fe4f-123">Dodawanie źródła stanie dla platformy .net Core:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="4fe4f-124">Dodaj stanie źródło repozytorium produktu Linux firmy Microsoft i zainstalować narzędzia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="4fe4f-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="4fe4f-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="4fe4f-126">Dodawanie źródła stanie dla platformy .net Core:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="4fe4f-127">Dodaj stanie źródło repozytorium produktu Linux firmy Microsoft i zainstalować narzędzia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="4fe4f-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="4fe4f-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="4fe4f-129">Dodawanie źródła stanie dla platformy .net Core:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="4fe4f-130">Dodaj stanie źródło repozytorium produktu Linux firmy Microsoft i zainstalować narzędzia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="4fe4f-131">Pisanie pierwszego polecenia AzCopy</span><span class="sxs-lookup"><span data-stu-id="4fe4f-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="4fe4f-132">Podstawowa składnia polecenia AzCopy Hello jest:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-132">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="4fe4f-133">Witaj następujące przykłady pokazują różne scenariusze kopiowania tooand danych z programu Microsoft Azure blob i plików.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-133">hello following examples demonstrate various scenarios for copying data tooand from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="4fe4f-134">Zobacz toohello `azcopy --help` menu, aby uzyskać szczegółowy opis hello parametrami używanymi w każdej próbki.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-134">Refer toohello `azcopy --help` menu for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="4fe4f-135">Obiekt blob: Pobierz</span><span class="sxs-lookup"><span data-stu-id="4fe4f-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="4fe4f-136">Pobieranie pojedynczego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="4fe4f-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="4fe4f-137">Jeśli hello folder `/mnt/myfiles` nie istnieje, narzędzie AzCopy tworzy go i pobiera `abc.txt ` do nowego folderu hello.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-137">If hello folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="4fe4f-138">Pobieranie pojedynczego obiektu blob z regionu pomocniczego</span><span class="sxs-lookup"><span data-stu-id="4fe4f-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="4fe4f-139">Należy pamiętać, że użytkownik musi mieć dostęp do odczytu magazynu geograficznie nadmiarowego włączone.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="4fe4f-140">Pobierz wszystkie obiekty BLOB</span><span class="sxs-lookup"><span data-stu-id="4fe4f-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="4fe4f-141">Załóżmy następujące hello obiekty BLOB znajdują się w określonym kontenerze hello:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-141">Assume hello following blobs reside in hello specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="4fe4f-142">Po wykonaniu operacji pobierania hello hello katalogu `/mnt/myfiles` obejmuje hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-142">After hello download operation, hello directory `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="4fe4f-143">Jeśli nie zostanie określona opcja `--recursive`, nie obiektu blob zostaną pobrane.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="4fe4f-144">Pobieranie obiektów blob z określonego prefiksu</span><span class="sxs-lookup"><span data-stu-id="4fe4f-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="4fe4f-145">Załóżmy następujące hello obiekty BLOB znajdują się w określonym kontenerze hello.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-145">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="4fe4f-146">Wszystkie obiekty BLOB rozpoczynający się od prefiksu powitania `a` zostaną pobrane.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-146">All blobs beginning with hello prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="4fe4f-147">Po wykonaniu operacji pobierania hello hello folderu `/mnt/myfiles` obejmuje hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-147">After hello download operation, hello folder `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="4fe4f-148">Prefiks Hello dotyczy katalogu wirtualnego toohello, który stanowi hello pierwsza część hello nazwa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-148">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="4fe4f-149">W powyższym przykładzie hello hello katalogu wirtualnego jest niezgodny hello określonego prefiksu, nie obiektu blob jest pobierana.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-149">In hello example shown above, hello virtual directory does not match hello specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="4fe4f-150">Ponadto, jeśli hello opcji `--recursive` nie zostanie określony, narzędzie AzCopy nie pobiera wszystkie obiekty BLOB.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-150">In addition, if hello option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="4fe4f-151">Ustawianie czasu ostatniej modyfikacji hello z toobe eksportowanych plików tak samo jak hello źródła obiektów blob</span><span class="sxs-lookup"><span data-stu-id="4fe4f-151">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="4fe4f-152">Można również wykluczyć obiekty BLOB z operacji pobierania hello na podstawie ich czasu ostatniej modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-152">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="4fe4f-153">Na przykład, jeśli chcesz tooexclude obiektów blob, których godzina ostatniej modyfikacji jest hello taką samą lub nowszą niż plik docelowy hello, dodać hello `--exclude-newer` opcji:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-153">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="4fe4f-154">Lub tooexclude obiektów blob, których godzina ostatniej modyfikacji jest hello tego samego lub starsze niż hello pliku docelowego, należy dodać hello `--exclude-older` opcji:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-154">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="4fe4f-155">Obiekt blob: Przekaż</span><span class="sxs-lookup"><span data-stu-id="4fe4f-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="4fe4f-156">Przekaż pojedynczy plik</span><span class="sxs-lookup"><span data-stu-id="4fe4f-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="4fe4f-157">Jeśli hello docelowy określony kontener nie istnieje, AzCopy tworzy go i przekazywanie hello pliku do niego.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-157">If hello specified destination container does not exist, AzCopy creates it and uploads hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="4fe4f-158">Przekaż pojedynczy plik toovirtual katalogu</span><span class="sxs-lookup"><span data-stu-id="4fe4f-158">Upload single file toovirtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="4fe4f-159">Jeśli hello określony katalog wirtualny nie istnieje, narzędzie AzCopy przekazuje hello pliku tooinclude hello katalogu wirtualnego w nazwie obiektu blob hello (*np.*, `vd/abc.txt` w powyższym przykładzie hello).</span><span class="sxs-lookup"><span data-stu-id="4fe4f-159">If hello specified virtual directory does not exist, AzCopy uploads hello file tooinclude hello virtual directory in hello blob name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="4fe4f-160">Przekaż wszystkie pliki</span><span class="sxs-lookup"><span data-stu-id="4fe4f-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="4fe4f-161">Określenie opcji `--recursive` przekazywanie zawartości hello hello określony rekursywnie magazynu tooBlob katalogu, co oznacza, jak również przekazać wszystkie podfoldery i pliki.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-161">Specifying option `--recursive` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="4fe4f-162">Na przykład załóżmy następujące hello pliki znajdują się w folderze `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-162">For instance, assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="4fe4f-163">Po wykonaniu operacji przekazywania hello hello kontener zawiera hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-163">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="4fe4f-164">Gdy hello opcja `--recursive` nie jest określona, tylko hello następujące trzy pliki są przesyłane:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-164">When hello option `--recursive` is not specified, only hello following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="4fe4f-165">Przekazywanie plików zgodnych z określonym wzorcem</span><span class="sxs-lookup"><span data-stu-id="4fe4f-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="4fe4f-166">Załóżmy następujące hello pliki znajdują się w folderze `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-166">Assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="4fe4f-167">Po wykonaniu operacji przekazywania hello hello kontener zawiera hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-167">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="4fe4f-168">Gdy hello opcji `--recursive` nie zostanie określony, narzędzie AzCopy pomija pliki, które są w katalogach podrzędnych:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-168">When hello option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="4fe4f-169">Określ typ zawartości MIME hello z docelowego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="4fe4f-169">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="4fe4f-170">Domyślnie narzędzie AzCopy ustawia typ zawartości hello docelowego obiektu blob zbyt`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-170">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="4fe4f-171">Jednak jawnie określić typ zawartości hello przy użyciu opcji hello `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-171">However, you can explicitly specify hello content type via hello option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="4fe4f-172">Ta składnia ustawia hello typ zawartości dla wszystkich obiektów blob w operacji przekazywania.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-172">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="4fe4f-173">Jeśli hello opcję `--set-content-type` jest określony bez wartości, a następnie ustawia AzCopy każdy obiekt blob lub pliku do typu zawartości zgodnie z tooits rozszerzenie pliku.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-173">If hello option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according tooits file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="4fe4f-174">Obiekt blob: kopiowania</span><span class="sxs-lookup"><span data-stu-id="4fe4f-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="4fe4f-175">Skopiuj pojedynczego obiektu blob w ramach konta magazynu</span><span class="sxs-lookup"><span data-stu-id="4fe4f-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="4fe4f-176">Podczas kopiowania obiektu blob bez — opcja synchronizacji kopii [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="4fe4f-177">Skopiuj pojedynczego obiektu blob na kontach magazynu</span><span class="sxs-lookup"><span data-stu-id="4fe4f-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="4fe4f-178">Podczas kopiowania obiektu blob bez — opcja synchronizacji kopii [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="4fe4f-179">Skopiuj pojedynczego obiektu blob z regionu pomocniczego tooprimary regionu</span><span class="sxs-lookup"><span data-stu-id="4fe4f-179">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="4fe4f-180">Należy pamiętać, że użytkownik musi mieć dostęp do odczytu magazynu geograficznie nadmiarowego włączone.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="4fe4f-181">Skopiuj pojedynczego obiektu blob i jego migawek wielu kont magazynu</span><span class="sxs-lookup"><span data-stu-id="4fe4f-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="4fe4f-182">Po wykonaniu operacji kopiowania hello kontenera docelowego hello obejmuje hello obiektów blob i jego migawek.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-182">After hello copy operation, hello target container includes hello blob and its snapshots.</span></span> <span data-ttu-id="4fe4f-183">Witaj kontener zawiera następujące hello jego migawki i obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-183">hello container includes hello following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="4fe4f-184">Synchronicznie skopiować wielu kont magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="4fe4f-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="4fe4f-185">Narzędzie AzCopy domyślnie kopiuje dane między dwoma punktami końcowymi magazynu asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="4fe4f-186">W związku z tym jest kopiowana hello kopiowania operacji działa w tle hello przy użyciu pojemności nieużywanej przepustowości ma umowy dotyczącej poziomu usług pod względem sposobu szybkiego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-186">Therefore, hello copy operation runs in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="4fe4f-187">Witaj `--sync-copy` opcji gwarantuje, że operacji kopiowania hello pobiera spójne szybkości.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-187">hello `--sync-copy` option ensures that hello copy operation gets consistent speed.</span></span> <span data-ttu-id="4fe4f-188">AzCopy wykonuje synchroniczne kopiowania hello pobierać obiekty BLOB hello toocopy z hello określone źródło toolocal pamięci, a następnie przekazywanie ich miejsce docelowe magazynu obiektów Blob toohello.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-188">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="4fe4f-189">`--sync-copy`może generować dodatkowe wyjście koszt w porównaniu tooasynchronous kopiowania.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-189">`--sync-copy` might generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="4fe4f-190">Witaj zalecane podejście jest toouse tej opcji w maszynie Wirtualnej platformy Azure, który znajduje się w hello tego samego regionu koszt wyjście tooavoid konta magazynu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-190">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="4fe4f-191">Plik: Pobierz</span><span class="sxs-lookup"><span data-stu-id="4fe4f-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="4fe4f-192">Pobierz pojedynczy plik</span><span class="sxs-lookup"><span data-stu-id="4fe4f-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="4fe4f-193">Jeśli hello określone źródło jest udział plików na platformę Azure, a następnie należy określić hello dokładnej nazwy pliku, (*np.* `abc.txt`) toodownload pojedynczy plik, lub określ opcję `--recursive` toodownload wszystkie pliki w udziale hello rekursywnie.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-193">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `--recursive` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="4fe4f-194">Próba toospecify zarówno wzorzec pliku, jak i opcja `--recursive` razem powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-194">Attempting toospecify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="4fe4f-195">Pobierz wszystkie pliki</span><span class="sxs-lookup"><span data-stu-id="4fe4f-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="4fe4f-196">Należy pamiętać, że puste foldery nie zostaną pobrane.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="4fe4f-197">Plik: Przekaż</span><span class="sxs-lookup"><span data-stu-id="4fe4f-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="4fe4f-198">Przekaż pojedynczy plik</span><span class="sxs-lookup"><span data-stu-id="4fe4f-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="4fe4f-199">Przekaż wszystkie pliki</span><span class="sxs-lookup"><span data-stu-id="4fe4f-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="4fe4f-200">Należy pamiętać, że wszystkie puste foldery nie zostały przekazane.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="4fe4f-201">Przekazywanie plików zgodnych z określonym wzorcem</span><span class="sxs-lookup"><span data-stu-id="4fe4f-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="4fe4f-202">Plik: kopiowania</span><span class="sxs-lookup"><span data-stu-id="4fe4f-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="4fe4f-203">Kopiowanie między udziałami plików</span><span class="sxs-lookup"><span data-stu-id="4fe4f-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="4fe4f-204">Podczas kopiowania plików między udziałami plików [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="4fe4f-205">Kopiowanie z tooblob udziału plików</span><span class="sxs-lookup"><span data-stu-id="4fe4f-205">Copy from file share tooblob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="4fe4f-206">Podczas kopiowania pliku z tooblob udziału pliku, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-206">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="4fe4f-207">Kopiowanie z udziału toofile obiektów blob</span><span class="sxs-lookup"><span data-stu-id="4fe4f-207">Copy from blob toofile share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="4fe4f-208">Podczas kopiowania pliku z udziału toofile obiektów blob, [po stronie serwera kopii](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operacja została wykonana.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-208">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="4fe4f-209">Synchronicznie kopiować pliki</span><span class="sxs-lookup"><span data-stu-id="4fe4f-209">Synchronously copy files</span></span>
<span data-ttu-id="4fe4f-210">Można określić hello `--sync-copy` synchronicznie opcję toocopy danych z magazynem tooFile magazynu, Magazyn plików tooBlob magazynu oraz tooFile magazynu obiektów Blob magazynu.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-210">You can specify hello `--sync-copy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously.</span></span> <span data-ttu-id="4fe4f-211">AzCopy uruchamia pobieranie hello źródła danych toolocal pamięci, a następnie przekazać go toodestination tej operacji.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-211">AzCopy runs this operation by downloading hello source data toolocal memory, and then uploading it toodestination.</span></span> <span data-ttu-id="4fe4f-212">W tym przypadku standardowe wyjście koszt dotyczy.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="4fe4f-213">Podczas kopiowania z pliku magazynu tooBlob magazynu, typu obiektu blob domyślne hello jest blokowych obiektów blob, użytkownik może określić opcję `/BlobType:page` toochange hello docelowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-213">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="4fe4f-214">Należy pamiętać, że `--sync-copy` może generować wyjście dodatkowych kosztów porównaniem tooasynchronous kopiowania.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-214">Note that `--sync-copy` might generate additional egress cost comparing tooasynchronous copy.</span></span> <span data-ttu-id="4fe4f-215">Witaj zalecane podejście jest toouse tej opcji w maszynie Wirtualnej platformy Azure, który znajduje się w hello tego samego regionu koszt wyjście tooavoid konta magazynu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-215">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="4fe4f-216">Inne funkcje AzCopy</span><span class="sxs-lookup"><span data-stu-id="4fe4f-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="4fe4f-217">Tylko skopiować dane, które nie istnieje w docelowym hello</span><span class="sxs-lookup"><span data-stu-id="4fe4f-217">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="4fe4f-218">Witaj `--exclude-older` i `--exclude-newer` parametrów pozwalają tooexclude starszej lub nowszej źródła zasobów zapobiega kopiowaniu odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-218">hello `--exclude-older` and `--exclude-newer` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="4fe4f-219">Jeśli chcesz tylko toocopy źródła zasobów, które nie istnieje w docelowym hello, można określić obu tych parametrów w hello polecenia programu AzCopy:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-219">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a><span data-ttu-id="4fe4f-220">Użyj konfiguracji parametry wiersza polecenia toospecify pliku</span><span class="sxs-lookup"><span data-stu-id="4fe4f-220">Use a configuration file toospecify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="4fe4f-221">Parametry wiersza polecenia AzCopy można uwzględnić w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="4fe4f-222">Procesy AzCopy hello parametrów w pliku hello tak, jakby były one określone w wierszu polecenia hello, wykonywanie bezpośrednich podstawienia z zawartością hello hello pliku.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-222">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="4fe4f-223">Załóżmy plik konfiguracji o nazwie `copyoperation`, który zawiera następujące wiersze hello.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-223">Assume a configuration file named `copyoperation`, that contains hello following lines.</span></span> <span data-ttu-id="4fe4f-224">Każdy parametr narzędzia AzCopy można określić w jednym wierszu.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="4fe4f-225">lub na oddzielnych wierszach:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="4fe4f-226">Narzędzie AzCopy wynik negatywny, jeśli parametr hello można podzielić na dwa wiersze, jak pokazano poniżej, aby uzyskać hello `--source-key` parametru:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-226">AzCopy fails if you split hello parameter across two lines, as shown here for hello `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="4fe4f-227">Określ sygnatury dostępu współdzielonego (SAS)</span><span class="sxs-lookup"><span data-stu-id="4fe4f-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="4fe4f-228">Można również określić sygnatury dostępu Współdzielonego w kontenerze hello identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-228">You can also specify a SAS on hello container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="4fe4f-229">Należy pamiętać, że narzędzie AzCopy aktualnie obsługuje tylko hello [SAS konta](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="4fe4f-229">Note that AzCopy currently only supports hello [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="4fe4f-230">Folder plików dziennika</span><span class="sxs-lookup"><span data-stu-id="4fe4f-230">Journal file folder</span></span>
<span data-ttu-id="4fe4f-231">Zawsze, gdy wystawiać tooAzCopy polecenia, sprawdza czy istnieje plik dziennika w folderze domyślnym hello, lub czy istnieje w folderze określonej za pomocą tej opcji.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-231">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="4fe4f-232">Jeśli plik dziennika hello nie istnieje w każdym miejscu, AzCopy traktuje operacji hello jako nowy i generuje nowy plik dziennika.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-232">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="4fe4f-233">Jeśli istnieje plik dziennika hello, AzCopy sprawdza, czy hello wiersza polecenia, które możesz wpisać zgodny hello wiersza polecenia w pliku dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-233">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="4fe4f-234">Jeśli dwa wiersze polecenia hello są zgodne, AzCopy wznawia hello nieukończone działania.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-234">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="4fe4f-235">Jeśli nie są zgodne, AzCopy monituje użytkownika tooeither Zastąp hello dziennika pliku toostart nowej operacji lub toocancel hello bieżącej operacji.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-235">If they do not match, AzCopy prompts user tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="4fe4f-236">Jeśli chcesz, aby toouse hello domyślna lokalizacja pliku dziennika hello:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-236">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="4fe4f-237">Jeśli pominięto opcję `--resume`, lub określ opcję `--resume` bez ścieżki folderu hello, jak pokazano powyżej, AzCopy tworzy plik dziennika hello w hello domyślnej lokalizacji, która jest `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-237">If you omit option `--resume`, or specify option `--resume` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="4fe4f-238">Jeśli plik dziennika hello już istnieje, AzCopy wznawia operację hello na podstawie hello pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-238">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="4fe4f-239">Jeśli chcesz, aby toospecify niestandardową lokalizację pliku dziennika hello:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-239">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="4fe4f-240">W tym przykładzie tworzy plik dziennika hello, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-240">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="4fe4f-241">Jeśli istnieje, narzędzie AzCopy wznawia operacji hello na podstawie hello pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-241">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="4fe4f-242">Tooresume operacji AzCopy, powtórz hello tego samego polecenia.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-242">If you want tooresume an AzCopy operation, repeat hello same command.</span></span> <span data-ttu-id="4fe4f-243">Narzędzie AzCopy w systemie Linux następnie wyświetli monit o potwierdzenie:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="4fe4f-244">Dzienniki pełne dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="4fe4f-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="4fe4f-245">Określ liczbę hello toostart jednoczesnych operacji</span><span class="sxs-lookup"><span data-stu-id="4fe4f-245">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="4fe4f-246">Opcja `--parallel-level` określa liczbę hello operacje kopiowania współbieżnych.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-246">Option `--parallel-level` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="4fe4f-247">Domyślnie narzędzie AzCopy uruchamia określoną liczbę jednoczesnych operacji tooincrease hello danych przeniesienie przepływności.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-247">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="4fe4f-248">Witaj liczba jednoczesnych operacji osiem godzin hello liczbę procesorów, masz.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-248">hello number of concurrent operations is equal eight times hello number of processors you have.</span></span> <span data-ttu-id="4fe4f-249">Jeśli używasz narzędzia AzCopy w niskiej przepustowości sieci, można określić mniejszą liczbę dla — poziom równoległe tooavoid niepowodzenie spowodowane przez konkurencji zasobów.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level tooavoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="4fe4f-250">tooview hello pełną listę parametrów narzędzia AzCopy, zapoznaj się z "azcopy--pomocy" menu.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-250">tooview hello complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="4fe4f-251">Znane problemy i najlepsze rozwiązania</span><span class="sxs-lookup"><span data-stu-id="4fe4f-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-hello-system"></a><span data-ttu-id="4fe4f-252">Błąd: Nie znaleziono .NET Core w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-252">Error: .NET Core is not found in hello system.</span></span>
<span data-ttu-id="4fe4f-253">Jeśli wystąpią komunikat o błędzie informujący, że oprogramowanie .NET Core nie jest zainstalowany w systemie hello hello ścieżki toohello .NET Core binary `dotnet` może brakować.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-253">If you encounter an error stating that .NET Core is not installed in hello system, hello PATH toohello .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="4fe4f-254">W kolejności tooaddress ten problem, Znajdź hello binary .NET Core w systemie hello:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-254">In order tooaddress this issue, find hello .NET Core binary in hello system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="4fe4f-255">To polecenie zwróci hello ścieżki toohello dotnet binarnego.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-255">This returns hello path toohello dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="4fe4f-256">Teraz Dodaj zmiennej PATH toohello tej ścieżki.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-256">Now add this path toohello PATH variable.</span></span> <span data-ttu-id="4fe4f-257">Sudo Edytuj secure_path toocontain hello ścieżki toohello dotnet binarne:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-257">For sudo, edit secure_path toocontain hello path toohello dotnet binary:</span></span>
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

<span data-ttu-id="4fe4f-258">W tym przykładzie zmienna secure_path odczytuje jako:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="4fe4f-259">Dla bieżącego użytkownika hello Edytuj.bash_profile/.profile tooinclude hello ścieżki toohello dotnet binarne w zmiennej PATH</span><span class="sxs-lookup"><span data-stu-id="4fe4f-259">For hello current user, edit .bash_profile/.profile tooinclude hello path toohello dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

<span data-ttu-id="4fe4f-260">Sprawdź, czy oprogramowanie .NET Core jest w ŚCIEŻCE:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="4fe4f-261">Błąd podczas instalowania narzędzia AzCopy</span><span class="sxs-lookup"><span data-stu-id="4fe4f-261">Error Installing AzCopy</span></span>
<span data-ttu-id="4fe4f-262">Jeśli wystąpią problemy z instalacją AzCopy, możesz spróbować toorun wyodrębnione narzędzie AzCopy przy użyciu skryptu bash hello w hello `azcopy` folderu.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-262">If you encounter issues with AzCopy installation, you may try toorun AzCopy using hello bash script in hello extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="4fe4f-263">Limit równoczesnych zapisów podczas kopiowania danych</span><span class="sxs-lookup"><span data-stu-id="4fe4f-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="4fe4f-264">Podczas kopiowania obiektów blob lub pliki z narzędzia AzCopy, należy pamiętać, że inna aplikacja może być modyfikowanie hello danych podczas kopiowania go.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="4fe4f-265">Jeśli to możliwe upewnij się, że hello dane, które są kopiowane nie jest modyfikowana podczas operacji kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-265">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="4fe4f-266">Na przykład podczas kopiowania wirtualnego dysku twardego skojarzonego z maszyny wirtualnej platformy Azure, upewnij się, że żadne inne aplikacje nie są obecnie zapisywania toohello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="4fe4f-267">Toodo dobrze to jest dzierżawa toobe zasobów hello skopiowane.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-267">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="4fe4f-268">Alternatywnie można najpierw Utwórz migawkę hello wirtualnego dysku twardego, a następnie skopiuj hello migawki.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-268">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="4fe4f-269">Jeśli nie można zapobiec innych aplikacji z zapisywania tooblobs lub plików podczas kopiowane są następnie pamiętać przez zadanie hello czasu hello zakończy, hello kopiowanych zasobów mogą już pełnej zgodności z hello źródła zasobów.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-269">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="4fe4f-270">Uruchom jedno wystąpienie AzCopy na jednej maszynie.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="4fe4f-271">Narzędzie AzCopy jest zaprojektowana toomaximize hello wykorzystania transferu danych hello tooaccelerate zasobów maszyny, zaleca się uruchomić tylko jedno wystąpienie AzCopy na jednej maszynie i określ opcję hello `--parallel-level` Jeśli potrzebujesz więcej jednoczesnych operacji.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-271">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="4fe4f-272">Aby uzyskać więcej informacji, wpisz `AzCopy --help parallel-level` hello wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="4fe4f-272">For more details, type `AzCopy --help parallel-level` at hello command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fe4f-273">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4fe4f-273">Next steps</span></span>
<span data-ttu-id="4fe4f-274">Aby uzyskać więcej informacji na temat usługi Azure Storage i AzCopy zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-274">For more information about Azure Storage and AzCopy, see hello following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="4fe4f-275">Dokumentacja magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="4fe4f-276">Wprowadzenie tooAzure magazynu</span><span class="sxs-lookup"><span data-stu-id="4fe4f-276">Introduction tooAzure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="4fe4f-277">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="4fe4f-277">Create a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="4fe4f-278">Zarządzanie obiektów blob z Eksploratora usługi Storage</span><span class="sxs-lookup"><span data-stu-id="4fe4f-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="4fe4f-279">Przy użyciu hello 2.0 interfejsu wiersza polecenia platformy Azure z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4fe4f-279">Using hello Azure CLI 2.0 with Azure Storage</span></span>](storage-azure-cli.md)
* [<span data-ttu-id="4fe4f-280">Jak toouse magazynu obiektów Blob w języku C++</span><span class="sxs-lookup"><span data-stu-id="4fe4f-280">How toouse Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="4fe4f-281">Jak toouse magazynu obiektów Blob w języku Java</span><span class="sxs-lookup"><span data-stu-id="4fe4f-281">How toouse Blob storage from Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="4fe4f-282">Jak toouse magazynu obiektów Blob w oprogramowaniu Node.js</span><span class="sxs-lookup"><span data-stu-id="4fe4f-282">How toouse Blob storage from Node.js</span></span>](storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="4fe4f-283">Jak toouse magazynu obiektów Blob w języku Python</span><span class="sxs-lookup"><span data-stu-id="4fe4f-283">How toouse Blob storage from Python</span></span>](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="4fe4f-284">Wpisy blogu magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="4fe4f-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="4fe4f-285">Anonsowanie AzCopy w wersji zapoznawczej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="4fe4f-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="4fe4f-286">Wprowadzenie Podgląd Biblioteka przepływu danych usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4fe4f-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="4fe4f-287">AzCopy: Wprowadzenie do kopiowania synchroniczne i dostosowane typ zawartości</span><span class="sxs-lookup"><span data-stu-id="4fe4f-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="4fe4f-288">Narzędzie AzCopy: Announcing ogólne dostępności 3.0 AzCopy oraz wersji zapoznawczej AzCopy 4.0 z tabeli i plik pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="4fe4f-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="4fe4f-289">Narzędzie AzCopy: Zoptymalizowana pod kątem scenariuszy kopii na dużą skalę</span><span class="sxs-lookup"><span data-stu-id="4fe4f-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="4fe4f-290">AzCopy: Obsługa dostęp do odczytu magazynu geograficznie nadmiarowego</span><span class="sxs-lookup"><span data-stu-id="4fe4f-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="4fe4f-291">Narzędzie AzCopy: Transfer danych za pomocą trybu ponownego uruchamiania i tokenu sygnatury dostępu Współdzielonego</span><span class="sxs-lookup"><span data-stu-id="4fe4f-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="4fe4f-292">Narzędzia AzCopy: Blob kopiowania między konta przy użyciu</span><span class="sxs-lookup"><span data-stu-id="4fe4f-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="4fe4f-293">Narzędzie AzCopy: Przekazywanie pobieranie plików dla obiektów blob Azure</span><span class="sxs-lookup"><span data-stu-id="4fe4f-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

