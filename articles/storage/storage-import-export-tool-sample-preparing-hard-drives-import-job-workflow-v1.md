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
ms.openlocfilehash: f836fc6104d8b4ad5660cb110a62f61b40b0b7ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="17ba3-103">Przykładowy przepływ pracy tooprepare dysków dla zadania importu</span><span class="sxs-lookup"><span data-stu-id="17ba3-103">Sample workflow tooprepare hard drives for an import job</span></span>
<span data-ttu-id="17ba3-104">W tym temacie przedstawiono hello Zakończ proces przygotowywania dysków dla zadania importu.</span><span class="sxs-lookup"><span data-stu-id="17ba3-104">This topic walks you through hello complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="17ba3-105">W tym przykładzie importuje powitania po danych na konto magazynu Azure okna o nazwie `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="17ba3-105">This example imports hello following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="17ba3-106">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="17ba3-106">Location</span></span>|<span data-ttu-id="17ba3-107">Opis</span><span class="sxs-lookup"><span data-stu-id="17ba3-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="17ba3-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="17ba3-108">H:\Video</span></span>|<span data-ttu-id="17ba3-109">Kolekcja filmów wideo, 5 TB w sumie.</span><span class="sxs-lookup"><span data-stu-id="17ba3-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="17ba3-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="17ba3-110">H:\Photo</span></span>|<span data-ttu-id="17ba3-111">Kolekcja zdjęć, 30 GB w sumie.</span><span class="sxs-lookup"><span data-stu-id="17ba3-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="17ba3-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="17ba3-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="17ba3-113">Obraz dysku A Blu-ray™, 25 GB.</span><span class="sxs-lookup"><span data-stu-id="17ba3-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="17ba3-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="17ba3-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="17ba3-115">Kolekcja plików muzycznych w udziale sieciowym, 10 GB w sumie.</span><span class="sxs-lookup"><span data-stu-id="17ba3-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="17ba3-116">zadania importu Hello zostaną zaimportowane te dane do następujących miejsc docelowych na koncie magazynu hello hello:</span><span class="sxs-lookup"><span data-stu-id="17ba3-116">hello import job will import this data into hello following destinations in hello storage account:</span></span>  
  
|<span data-ttu-id="17ba3-117">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="17ba3-117">Source</span></span>|<span data-ttu-id="17ba3-118">Katalog wirtualny docelowego lub obiektu blob</span><span class="sxs-lookup"><span data-stu-id="17ba3-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="17ba3-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="17ba3-119">H:\Video</span></span>|<span data-ttu-id="17ba3-120">https://mystorageaccount.blob.Core.Windows.NET/Video</span><span class="sxs-lookup"><span data-stu-id="17ba3-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="17ba3-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="17ba3-121">H:\Photo</span></span>|<span data-ttu-id="17ba3-122">https://mystorageaccount.blob.Core.Windows.NET/Photo</span><span class="sxs-lookup"><span data-stu-id="17ba3-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="17ba3-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="17ba3-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="17ba3-124">https://mystorageaccount.blob.Core.Windows.NET/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="17ba3-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="17ba3-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="17ba3-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="17ba3-126">https://mystorageaccount.blob.Core.Windows.NET/Music</span><span class="sxs-lookup"><span data-stu-id="17ba3-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="17ba3-127">Do tego mapowania hello pliku `H:\Video\Drama\GreatMovie.mov` będzie toohello importowanych obiektów blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="17ba3-127">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="17ba3-128">Następnie toodetermine liczbę dysków twardych są potrzebne, obliczeń hello rozmiar danych hello:</span><span class="sxs-lookup"><span data-stu-id="17ba3-128">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="17ba3-129">Na przykład dwa 3TB dyski twarde powinny być wystarczające.</span><span class="sxs-lookup"><span data-stu-id="17ba3-129">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="17ba3-130">Jednak ponieważ katalog źródłowy hello `H:\Video` ma 5TB danych i pojemności pojedynczego dysku twardego w tylko 3TB jest konieczne toobreak `H:\Video` na dwa katalogi mniejszych przed uruchomieniem hello narzędzia importu/eksportu pakietu Microsoft Azure: `H:\Video1` i `H:\Video2`.</span><span class="sxs-lookup"><span data-stu-id="17ba3-130">However, since hello source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary toobreak `H:\Video` into two smaller directories before running hello Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="17ba3-131">Ten krok powoduje hello następujące katalogi źródłowe:</span><span class="sxs-lookup"><span data-stu-id="17ba3-131">This step yields hello following source directories:</span></span>  
  
|<span data-ttu-id="17ba3-132">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="17ba3-132">Location</span></span>|<span data-ttu-id="17ba3-133">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="17ba3-133">Size</span></span>|<span data-ttu-id="17ba3-134">Katalog wirtualny docelowego lub obiektu blob</span><span class="sxs-lookup"><span data-stu-id="17ba3-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="17ba3-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="17ba3-135">H:\Video1</span></span>|<span data-ttu-id="17ba3-136">2.5 TB</span><span class="sxs-lookup"><span data-stu-id="17ba3-136">2.5TB</span></span>|<span data-ttu-id="17ba3-137">https://mystorageaccount.blob.Core.Windows.NET/Video</span><span class="sxs-lookup"><span data-stu-id="17ba3-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="17ba3-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="17ba3-138">H:\Video2</span></span>|<span data-ttu-id="17ba3-139">2.5 TB</span><span class="sxs-lookup"><span data-stu-id="17ba3-139">2.5TB</span></span>|<span data-ttu-id="17ba3-140">https://mystorageaccount.blob.Core.Windows.NET/Video</span><span class="sxs-lookup"><span data-stu-id="17ba3-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="17ba3-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="17ba3-141">H:\Photo</span></span>|<span data-ttu-id="17ba3-142">30 GB</span><span class="sxs-lookup"><span data-stu-id="17ba3-142">30GB</span></span>|<span data-ttu-id="17ba3-143">https://mystorageaccount.blob.Core.Windows.NET/Photo</span><span class="sxs-lookup"><span data-stu-id="17ba3-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="17ba3-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="17ba3-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="17ba3-145">25 GB</span><span class="sxs-lookup"><span data-stu-id="17ba3-145">25GB</span></span>|<span data-ttu-id="17ba3-146">https://mystorageaccount.blob.Core.Windows.NET/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="17ba3-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="17ba3-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="17ba3-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="17ba3-148">10GB</span><span class="sxs-lookup"><span data-stu-id="17ba3-148">10GB</span></span>|<span data-ttu-id="17ba3-149">https://mystorageaccount.blob.Core.Windows.NET/Music</span><span class="sxs-lookup"><span data-stu-id="17ba3-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="17ba3-150">Należy pamiętać, że nawet jeśli hello `H:\Video`katalogu podzielonego tootwo katalogów, wskazywały toohello sam docelowy katalog wirtualny na koncie magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="17ba3-150">Note that even though hello `H:\Video`directory has been split tootwo directories, they point toohello same destination virtual directory in hello storage account.</span></span> <span data-ttu-id="17ba3-151">Dzięki temu wszystkie pliki wideo są obsługiwane pod jedną `video` kontenera na koncie magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="17ba3-151">This way, all video files are maintained under a single `video` container in hello storage account.</span></span>  
  
 <span data-ttu-id="17ba3-152">Następnie hello powyżej źródło katalogi są równomiernie przekazany toohello dwóch dysków twardych:</span><span class="sxs-lookup"><span data-stu-id="17ba3-152">Next, hello above source directories are evenly distributed toohello two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="17ba3-153">Dysk twardy</span><span class="sxs-lookup"><span data-stu-id="17ba3-153">Hard drive</span></span>|<span data-ttu-id="17ba3-154">Katalogi źródłowe</span><span class="sxs-lookup"><span data-stu-id="17ba3-154">Source directories</span></span>|<span data-ttu-id="17ba3-155">Całkowity rozmiar</span><span class="sxs-lookup"><span data-stu-id="17ba3-155">Total size</span></span>|  
|<span data-ttu-id="17ba3-156">Pierwszy dysku</span><span class="sxs-lookup"><span data-stu-id="17ba3-156">First Drive</span></span>|<span data-ttu-id="17ba3-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="17ba3-157">H:\Video1</span></span>|<span data-ttu-id="17ba3-158">2,5 TB + 30 GB</span><span class="sxs-lookup"><span data-stu-id="17ba3-158">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="17ba3-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="17ba3-159">H:\Photo</span></span>||  
|<span data-ttu-id="17ba3-160">Dysku na sekundę</span><span class="sxs-lookup"><span data-stu-id="17ba3-160">Second Drive</span></span>|<span data-ttu-id="17ba3-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="17ba3-161">H:\Video2</span></span>|<span data-ttu-id="17ba3-162">2,5 TB + 35 GB</span><span class="sxs-lookup"><span data-stu-id="17ba3-162">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="17ba3-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="17ba3-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="17ba3-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="17ba3-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="17ba3-165">Ponadto można ustawić hello następujące metadane dla wszystkich plików:</span><span class="sxs-lookup"><span data-stu-id="17ba3-165">In addition, you can set hello following metadata for all files:</span></span>  
  
-   <span data-ttu-id="17ba3-166">**UploadMethod:** usługi Import/Eksport systemu Windows Azure</span><span class="sxs-lookup"><span data-stu-id="17ba3-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="17ba3-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="17ba3-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="17ba3-168">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="17ba3-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="17ba3-169">metadane tooset plików hello zaimportowane, Utwórz plik tekstowy `c:\WAImportExport\SampleMetadata.txt`, z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="17ba3-169">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="17ba3-170">Można również ustawić niektórych właściwości hello `FavoriteMovie.ISO` obiektu blob:</span><span class="sxs-lookup"><span data-stu-id="17ba3-170">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="17ba3-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="17ba3-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="17ba3-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==</span><span class="sxs-lookup"><span data-stu-id="17ba3-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="17ba3-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="17ba3-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="17ba3-174">tooset te właściwości, Utwórz plik tekstowy `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="17ba3-174">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="17ba3-175">Teraz wszystko jest gotowe toorun hello Azure narzędzie importu/eksportu tooprepare hello dwóch dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="17ba3-175">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span> <span data-ttu-id="17ba3-176">Należy pamiętać, że:</span><span class="sxs-lookup"><span data-stu-id="17ba3-176">Note that:</span></span>  
  
-   <span data-ttu-id="17ba3-177">Witaj pierwszego dysku jest zainstalowany jako dysku X.</span><span class="sxs-lookup"><span data-stu-id="17ba3-177">hello first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="17ba3-178">drugi dysk Hello jest zainstalowany jako dysk Y.</span><span class="sxs-lookup"><span data-stu-id="17ba3-178">hello second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="17ba3-179">Witaj klucza dla konta magazynu hello `mystorageaccount` jest `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="17ba3-179">hello key for hello storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="17ba3-180">Przygotowywanie dysku do zaimportowania podczas wstępnego ładowania danych</span><span class="sxs-lookup"><span data-stu-id="17ba3-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="17ba3-181">Jeśli zaimportowane toobe danych hello jest już obecny na powitania dysku, użyj /skipwrite flagi hello.</span><span class="sxs-lookup"><span data-stu-id="17ba3-181">If hello data toobe imported is already present on hello disk, use hello flag /skipwrite.</span></span> <span data-ttu-id="17ba3-182">Wartość /t i /srcdir powinny wskazywać dysku toohello przygotowanym do importu.</span><span class="sxs-lookup"><span data-stu-id="17ba3-182">Value of /t and /srcdir both should point toohello disk being prepared for import.</span></span> <span data-ttu-id="17ba3-183">Jeśli nie wszystkie hello danych na dysku hello musi toogo toohello tego samego katalogu wirtualnego w docelowym lub głównego konta magazynu hello, hello wykonywania polecenia takie same dla każdego katalogu oddzielnie zachowuje wartość hello/identyfikator tej samej przez wszystkie elementy.</span><span class="sxs-lookup"><span data-stu-id="17ba3-183">If not all hello data on hello disk needs toogo toohello same destination virtual directory or root of hello storage account, run hello same command for each directory separately keeping hello value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="17ba3-184">Nie określaj/format, jak go spowoduje wyczyszczenie danych hello na powitania dysku.</span><span class="sxs-lookup"><span data-stu-id="17ba3-184">Do not specify /format as it will wipe hello data on hello disk.</span></span> <span data-ttu-id="17ba3-185">Można określić / szyfrowania lub /bk w zależności od tego, czy dysk hello jest już zaszyfrowane lub nie.</span><span class="sxs-lookup"><span data-stu-id="17ba3-185">You can specify /encrypt or /bk depending on whether hello disk is already encrypted or not.</span></span> 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="17ba3-186">Skopiuj sesje — najpierw dysków</span><span class="sxs-lookup"><span data-stu-id="17ba3-186">Copy sessions - first drive</span></span>

<span data-ttu-id="17ba3-187">Dla pierwszego dysku hello Uruchom hello Azure narzędzie importu/eksportu źródła dwukrotnie hello toocopy dwa katalogi:</span><span class="sxs-lookup"><span data-stu-id="17ba3-187">For hello first drive, run hello Azure Import/Export Tool twice toocopy hello two source directories:</span></span>  

<span data-ttu-id="17ba3-188">**Najpierw skopiować sesji**</span><span class="sxs-lookup"><span data-stu-id="17ba3-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="17ba3-189">**Druga kopia sesji**</span><span class="sxs-lookup"><span data-stu-id="17ba3-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="17ba3-190">Skopiuj sesji — w drugim dysku</span><span class="sxs-lookup"><span data-stu-id="17ba3-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="17ba3-191">Dla hello drugiego dysku, uruchom hello Azure narzędzie importu/eksportu trzy razy, po wszystkich hello źródła katalogów i raz dla autonomicznej hello Blu-Ray™ pliku obrazu):</span><span class="sxs-lookup"><span data-stu-id="17ba3-191">For hello second drive, run hello Azure Import/Export Tool three times, once each for hello source directories, and once for hello standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="17ba3-192">**Najpierw skopiować sesji**</span><span class="sxs-lookup"><span data-stu-id="17ba3-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="17ba3-193">**Druga kopia sesji**</span><span class="sxs-lookup"><span data-stu-id="17ba3-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="17ba3-194">**Trzeci sesji kopiowania**</span><span class="sxs-lookup"><span data-stu-id="17ba3-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="17ba3-195">Skopiuj zakończenia sesji</span><span class="sxs-lookup"><span data-stu-id="17ba3-195">Copy session completion</span></span>

<span data-ttu-id="17ba3-196">Po hello kopiowania sesji została ukończona, można odłączyć Witaj dwie stacje z komputera kopiowania hello i wysłać je toohello odpowiednie centrum danych systemu Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="17ba3-196">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Windows Azure data center.</span></span> <span data-ttu-id="17ba3-197">Będzie przekazać hello dwa pliki dziennika, `FirstDrive.jrn` i `SecondDrive.jrn`, podczas tworzenia zadania importu hello w hello [portalu zarządzania pakietu Windows Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="17ba3-197">You'll upload hello two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create hello import job in hello [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="17ba3-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="17ba3-198">Next steps</span></span>

* [<span data-ttu-id="17ba3-199">Przygotowywanie dysków twardych do zadania importu</span><span class="sxs-lookup"><span data-stu-id="17ba3-199">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="17ba3-200">Krótki przewodnik dla często używanych poleceń</span><span class="sxs-lookup"><span data-stu-id="17ba3-200">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference-v1.md) 
