---
title: "aaaSample przepływu pracy tooprep dyski twarde dla Import/Eksport Azure Importuj zadanie - v1 | Dokumentacja firmy Microsoft"
description: "Zobacz wskazówki dla hello Zakończ proces przygotowywania dysków dla zadania importu w hello usługi Import/Eksport Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: eb77831a88c16c14838179a6432ddb06503067dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="2191a-103">Przykładowy przepływ pracy tooprepare dysków dla zadania importu</span><span class="sxs-lookup"><span data-stu-id="2191a-103">Sample workflow tooprepare hard drives for an import job</span></span>
<span data-ttu-id="2191a-104">W tym temacie przedstawiono hello Zakończ proces przygotowywania dysków dla zadania importu.</span><span class="sxs-lookup"><span data-stu-id="2191a-104">This topic walks you through hello complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="2191a-105">W tym przykładzie importuje powitania po danych na konto magazynu Azure okna o nazwie `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="2191a-105">This example imports hello following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="2191a-106">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="2191a-106">Location</span></span>|<span data-ttu-id="2191a-107">Opis</span><span class="sxs-lookup"><span data-stu-id="2191a-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="2191a-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="2191a-108">H:\Video</span></span>|<span data-ttu-id="2191a-109">Kolekcja filmów wideo, 5 TB w sumie.</span><span class="sxs-lookup"><span data-stu-id="2191a-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="2191a-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="2191a-110">H:\Photo</span></span>|<span data-ttu-id="2191a-111">Kolekcja zdjęć, 30 GB w sumie.</span><span class="sxs-lookup"><span data-stu-id="2191a-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="2191a-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="2191a-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="2191a-113">Obraz dysku A Blu-ray™, 25 GB.</span><span class="sxs-lookup"><span data-stu-id="2191a-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="2191a-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="2191a-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="2191a-115">Kolekcja plików muzycznych w udziale sieciowym, 10 GB w sumie.</span><span class="sxs-lookup"><span data-stu-id="2191a-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="2191a-116">zadania importu Hello importuje dane do następujących miejsc docelowych na koncie magazynu hello hello:</span><span class="sxs-lookup"><span data-stu-id="2191a-116">hello import job imports this data into hello following destinations in hello storage account:</span></span>  
  
|<span data-ttu-id="2191a-117">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="2191a-117">Source</span></span>|<span data-ttu-id="2191a-118">Katalog wirtualny docelowego lub obiektu blob</span><span class="sxs-lookup"><span data-stu-id="2191a-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="2191a-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="2191a-119">H:\Video</span></span>|<span data-ttu-id="2191a-120">https://mystorageaccount.blob.Core.Windows.NET/Video</span><span class="sxs-lookup"><span data-stu-id="2191a-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="2191a-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="2191a-121">H:\Photo</span></span>|<span data-ttu-id="2191a-122">https://mystorageaccount.blob.Core.Windows.NET/Photo</span><span class="sxs-lookup"><span data-stu-id="2191a-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="2191a-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="2191a-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="2191a-124">https://mystorageaccount.blob.Core.Windows.NET/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="2191a-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="2191a-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="2191a-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="2191a-126">https://mystorageaccount.blob.Core.Windows.NET/Music</span><span class="sxs-lookup"><span data-stu-id="2191a-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="2191a-127">Do tego mapowania hello pliku `H:\Video\Drama\GreatMovie.mov` toohello importowanych obiektów blob jest `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="2191a-127">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` is imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="2191a-128">Następnie toodetermine liczbę dysków twardych są potrzebne, obliczeń hello rozmiar danych hello:</span><span class="sxs-lookup"><span data-stu-id="2191a-128">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="2191a-129">Na przykład dwa 3 TB dyski twarde powinny być wystarczające.</span><span class="sxs-lookup"><span data-stu-id="2191a-129">For this example, two 3-TB hard drives should be sufficient.</span></span> <span data-ttu-id="2191a-130">Jednak ponieważ katalog źródłowy hello `H:\Video` ma 5 TB danych i pojemności pojedynczego dysku twardego w tylko 3 TB jest konieczne toobreak `H:\Video` na dwa katalogi mniejsze: `H:\Video1` i `H:\Video2`, zanim uruchomiona hello firmy Microsoft Narzędzie importu/eksportu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2191a-130">However, since hello source directory `H:\Video` has 5 TB of data and your single hard drive's capacity is only 3 TB, it's necessary toobreak `H:\Video` into two smaller directories: `H:\Video1` and `H:\Video2`, before running hello Microsoft Azure Import/Export Tool.</span></span> <span data-ttu-id="2191a-131">Ten krok powoduje hello następujące katalogi źródłowe:</span><span class="sxs-lookup"><span data-stu-id="2191a-131">This step yields hello following source directories:</span></span>  
  
|<span data-ttu-id="2191a-132">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="2191a-132">Location</span></span>|<span data-ttu-id="2191a-133">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="2191a-133">Size</span></span>|<span data-ttu-id="2191a-134">Katalog wirtualny docelowego lub obiektu blob</span><span class="sxs-lookup"><span data-stu-id="2191a-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="2191a-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="2191a-135">H:\Video1</span></span>|<span data-ttu-id="2191a-136">2,5 TB</span><span class="sxs-lookup"><span data-stu-id="2191a-136">2.5 TB</span></span>|<span data-ttu-id="2191a-137">https://mystorageaccount.blob.Core.Windows.NET/Video</span><span class="sxs-lookup"><span data-stu-id="2191a-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="2191a-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="2191a-138">H:\Video2</span></span>|<span data-ttu-id="2191a-139">2,5 TB</span><span class="sxs-lookup"><span data-stu-id="2191a-139">2.5 TB</span></span>|<span data-ttu-id="2191a-140">https://mystorageaccount.blob.Core.Windows.NET/Video</span><span class="sxs-lookup"><span data-stu-id="2191a-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="2191a-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="2191a-141">H:\Photo</span></span>|<span data-ttu-id="2191a-142">30 GB</span><span class="sxs-lookup"><span data-stu-id="2191a-142">30 GB</span></span>|<span data-ttu-id="2191a-143">https://mystorageaccount.blob.Core.Windows.NET/Photo</span><span class="sxs-lookup"><span data-stu-id="2191a-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="2191a-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="2191a-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="2191a-145">25 GB</span><span class="sxs-lookup"><span data-stu-id="2191a-145">25 GB</span></span>|<span data-ttu-id="2191a-146">https://mystorageaccount.blob.Core.Windows.NET/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="2191a-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="2191a-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="2191a-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="2191a-148">10 GB</span><span class="sxs-lookup"><span data-stu-id="2191a-148">10 GB</span></span>|<span data-ttu-id="2191a-149">https://mystorageaccount.blob.Core.Windows.NET/Music</span><span class="sxs-lookup"><span data-stu-id="2191a-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="2191a-150">Mimo że hello `H:\Video`katalogu podzielonego tootwo katalogów, wskazywały toohello sam docelowy katalog wirtualny na koncie magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="2191a-150">Even though hello `H:\Video`directory has been split tootwo directories, they point toohello same destination virtual directory in hello storage account.</span></span> <span data-ttu-id="2191a-151">Dzięki temu wszystkie pliki wideo są obsługiwane pod jedną `video` kontenera na koncie magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="2191a-151">This way, all video files are maintained under a single `video` container in hello storage account.</span></span>  
  
 <span data-ttu-id="2191a-152">Następnie poprzedniej katalogi źródłowe hello są równomiernie rozłożony toohello dwóch dysków twardych:</span><span class="sxs-lookup"><span data-stu-id="2191a-152">Next, hello previous source directories are evenly distributed toohello two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="2191a-153">Dysk twardy</span><span class="sxs-lookup"><span data-stu-id="2191a-153">Hard drive</span></span>|<span data-ttu-id="2191a-154">Katalogi źródłowe</span><span class="sxs-lookup"><span data-stu-id="2191a-154">Source directories</span></span>|<span data-ttu-id="2191a-155">Całkowity rozmiar</span><span class="sxs-lookup"><span data-stu-id="2191a-155">Total size</span></span>|  
|<span data-ttu-id="2191a-156">Pierwszy dysku</span><span class="sxs-lookup"><span data-stu-id="2191a-156">First Drive</span></span>|<span data-ttu-id="2191a-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="2191a-157">H:\Video1</span></span>|<span data-ttu-id="2191a-158">2,5 TB + 30 GB</span><span class="sxs-lookup"><span data-stu-id="2191a-158">2.5 TB + 30 GB</span></span>|  
||<span data-ttu-id="2191a-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="2191a-159">H:\Photo</span></span>||  
|<span data-ttu-id="2191a-160">Dysku na sekundę</span><span class="sxs-lookup"><span data-stu-id="2191a-160">Second Drive</span></span>|<span data-ttu-id="2191a-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="2191a-161">H:\Video2</span></span>|<span data-ttu-id="2191a-162">2,5 TB + 35 GB</span><span class="sxs-lookup"><span data-stu-id="2191a-162">2.5 TB + 35 GB</span></span>|  
||<span data-ttu-id="2191a-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="2191a-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="2191a-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="2191a-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="2191a-165">Ponadto można ustawić hello następujące metadane dla wszystkich plików:</span><span class="sxs-lookup"><span data-stu-id="2191a-165">In addition, you can set hello following metadata for all files:</span></span>  
  
-   <span data-ttu-id="2191a-166">**UploadMethod:** usługi Import/Eksport systemu Windows Azure</span><span class="sxs-lookup"><span data-stu-id="2191a-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="2191a-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="2191a-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="2191a-168">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="2191a-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="2191a-169">metadane tooset plików hello zaimportowane, Utwórz plik tekstowy `c:\WAImportExport\SampleMetadata.txt`, z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="2191a-169">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="2191a-170">Można również ustawić niektórych właściwości hello `FavoriteMovie.ISO` obiektu blob:</span><span class="sxs-lookup"><span data-stu-id="2191a-170">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="2191a-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="2191a-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="2191a-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==</span><span class="sxs-lookup"><span data-stu-id="2191a-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="2191a-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="2191a-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="2191a-174">tooset te właściwości, Utwórz plik tekstowy `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="2191a-174">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="2191a-175">Teraz wszystko jest gotowe toorun hello Azure narzędzie importu/eksportu tooprepare hello dwóch dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="2191a-175">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span> <span data-ttu-id="2191a-176">Należy pamiętać, że:</span><span class="sxs-lookup"><span data-stu-id="2191a-176">Note that:</span></span>  
  
-   <span data-ttu-id="2191a-177">Witaj pierwszego dysku jest zainstalowany jako dysku X.</span><span class="sxs-lookup"><span data-stu-id="2191a-177">hello first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="2191a-178">drugi dysk Hello jest zainstalowany jako dysk Y.</span><span class="sxs-lookup"><span data-stu-id="2191a-178">hello second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="2191a-179">Witaj klucza dla konta magazynu hello `mystorageaccount` jest `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="2191a-179">hello key for hello storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="2191a-180">Przygotowywanie dysku do zaimportowania podczas wstępnego ładowania danych</span><span class="sxs-lookup"><span data-stu-id="2191a-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="2191a-181">Jeśli zaimportowane toobe danych hello jest już obecny na powitania dysku, użyj /skipwrite flagi hello.</span><span class="sxs-lookup"><span data-stu-id="2191a-181">If hello data toobe imported is already present on hello disk, use hello flag /skipwrite.</span></span> <span data-ttu-id="2191a-182">wartość Hello /t i /srcdir powinna zarówno dysku punktu toohello przygotowanym do importu.</span><span class="sxs-lookup"><span data-stu-id="2191a-182">hello value of /t and /srcdir should both point toohello disk being prepared for import.</span></span> <span data-ttu-id="2191a-183">Jeśli nie będzie wszystkie toobe danych hello zaimportowane toohello tego samego katalogu wirtualnego w docelowym lub głównego hello konta magazynu, uruchom hello same polecenie dla każdego katalogu docelowego oddzielnie, aktualizowania wartości hello/identyfikator hello sam przez wszystkie elementy.</span><span class="sxs-lookup"><span data-stu-id="2191a-183">If all of hello data toobe imported is not going toohello same destination virtual directory or root of hello storage account, run hello same command for each destination directory separately, keeping hello value of /id hello same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="2191a-184">Nie określaj/format, jak go spowoduje wyczyszczenie danych hello na powitania dysku.</span><span class="sxs-lookup"><span data-stu-id="2191a-184">Do not specify /format as it will wipe hello data on hello disk.</span></span> <span data-ttu-id="2191a-185">Można określić / szyfrowania lub /bk w zależności od tego, czy dysk hello jest już zaszyfrowane lub nie.</span><span class="sxs-lookup"><span data-stu-id="2191a-185">You can specify /encrypt or /bk depending on whether hello disk is already encrypted or not.</span></span> 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="2191a-186">Skopiuj sesje — najpierw dysków</span><span class="sxs-lookup"><span data-stu-id="2191a-186">Copy sessions - first drive</span></span>

<span data-ttu-id="2191a-187">Dla pierwszego dysku hello Uruchom hello Azure narzędzie importu/eksportu źródła dwukrotnie hello toocopy dwa katalogi:</span><span class="sxs-lookup"><span data-stu-id="2191a-187">For hello first drive, run hello Azure Import/Export Tool twice toocopy hello two source directories:</span></span>  

<span data-ttu-id="2191a-188">**Najpierw skopiować sesji**</span><span class="sxs-lookup"><span data-stu-id="2191a-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="2191a-189">**Druga kopia sesji**</span><span class="sxs-lookup"><span data-stu-id="2191a-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="2191a-190">Skopiuj sesji — w drugim dysku</span><span class="sxs-lookup"><span data-stu-id="2191a-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="2191a-191">Dla hello drugiego dysku, uruchom hello Azure narzędzie importu/eksportu trzy razy, po wszystkich hello źródła katalogów i raz dla autonomicznej hello Blu-Ray™ pliku obrazu):</span><span class="sxs-lookup"><span data-stu-id="2191a-191">For hello second drive, run hello Azure Import/Export Tool three times, once each for hello source directories, and once for hello standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="2191a-192">**Najpierw skopiować sesji**</span><span class="sxs-lookup"><span data-stu-id="2191a-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="2191a-193">**Druga kopia sesji**</span><span class="sxs-lookup"><span data-stu-id="2191a-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="2191a-194">**Trzeci sesji kopiowania**</span><span class="sxs-lookup"><span data-stu-id="2191a-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="2191a-195">Skopiuj zakończenia sesji</span><span class="sxs-lookup"><span data-stu-id="2191a-195">Copy session completion</span></span>

<span data-ttu-id="2191a-196">Po hello kopiowania sesji została ukończona, można odłączyć Witaj dwie stacje z komputera kopiowania hello i wysłać je toohello odpowiednie centrum danych systemu Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="2191a-196">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Windows Azure data center.</span></span> <span data-ttu-id="2191a-197">Przekaż hello dwa pliki dziennika, `FirstDrive.jrn` i `SecondDrive.jrn`, podczas tworzenia zadania importu hello w hello [portalu Windows Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="2191a-197">Upload hello two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create hello import job in hello [Windows Azure portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="2191a-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2191a-198">Next steps</span></span>

* [<span data-ttu-id="2191a-199">Przygotowywanie dysków twardych do zadania importu</span><span class="sxs-lookup"><span data-stu-id="2191a-199">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="2191a-200">Krótki przewodnik dla często używanych poleceń</span><span class="sxs-lookup"><span data-stu-id="2191a-200">Quick reference for frequently used commands</span></span>](../storage-import-export-tool-quick-reference-v1.md) 
