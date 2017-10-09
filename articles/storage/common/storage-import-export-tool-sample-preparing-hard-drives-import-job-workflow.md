---
title: "aaaSample przepływu pracy tooprep dyski twarde dla Import/Eksport Azure Importuj zadanie | Dokumentacja firmy Microsoft"
description: "Zobacz wskazówki dla hello Zakończ proces przygotowywania dysków dla zadania importu w hello usługi Import/Eksport Azure."
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
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: fa7f36300b35b81757523de4960fd583bd4bf305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="89d79-103">Przykładowy przepływ pracy tooprepare dysków dla zadania importu</span><span class="sxs-lookup"><span data-stu-id="89d79-103">Sample workflow tooprepare hard drives for an import job</span></span>

<span data-ttu-id="89d79-104">W tym artykule przedstawiono hello Zakończ proces przygotowywania dysków dla zadania importu.</span><span class="sxs-lookup"><span data-stu-id="89d79-104">This article walks you through hello complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="89d79-105">Dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="89d79-105">Sample data</span></span>

<span data-ttu-id="89d79-106">W tym przykładzie importuje powitania po danych do konta magazynu platformy Azure o nazwie `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="89d79-106">This example imports hello following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="89d79-107">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="89d79-107">Location</span></span>|<span data-ttu-id="89d79-108">Opis</span><span class="sxs-lookup"><span data-stu-id="89d79-108">Description</span></span>|<span data-ttu-id="89d79-109">Rozmiar danych</span><span class="sxs-lookup"><span data-stu-id="89d79-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="89d79-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="89d79-110">H:\Video\\</span></span> |<span data-ttu-id="89d79-111">Kolekcja filmów wideo</span><span class="sxs-lookup"><span data-stu-id="89d79-111">A collection of videos</span></span>|<span data-ttu-id="89d79-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="89d79-112">12 TB</span></span>|
|<span data-ttu-id="89d79-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="89d79-113">H:\Photo\\</span></span> |<span data-ttu-id="89d79-114">Kolekcja zdjęć</span><span class="sxs-lookup"><span data-stu-id="89d79-114">A collection of photos</span></span>|<span data-ttu-id="89d79-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="89d79-115">30 GB</span></span>|
|<span data-ttu-id="89d79-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="89d79-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="89d79-117">Obraz dysku A Blu-ray™</span><span class="sxs-lookup"><span data-stu-id="89d79-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="89d79-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="89d79-118">25 GB</span></span>|
|<span data-ttu-id="89d79-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="89d79-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="89d79-120">Kolekcja plików muzycznych w udziale sieciowym</span><span class="sxs-lookup"><span data-stu-id="89d79-120">A collection of music files on a network share</span></span>|<span data-ttu-id="89d79-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="89d79-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="89d79-122">Miejsca docelowe konto magazynu</span><span class="sxs-lookup"><span data-stu-id="89d79-122">Storage account destinations</span></span>

<span data-ttu-id="89d79-123">zadania importu Hello zostaną zaimportowane hello danych do następujących miejsc docelowych na koncie magazynu hello hello:</span><span class="sxs-lookup"><span data-stu-id="89d79-123">hello import job will import hello data into hello following destinations in hello storage account:</span></span>

|<span data-ttu-id="89d79-124">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="89d79-124">Source</span></span>|<span data-ttu-id="89d79-125">Katalog wirtualny docelowego lub obiektu blob</span><span class="sxs-lookup"><span data-stu-id="89d79-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="89d79-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="89d79-126">H:\Video\\</span></span> |<span data-ttu-id="89d79-127">wideo /</span><span class="sxs-lookup"><span data-stu-id="89d79-127">video/</span></span>|
|<span data-ttu-id="89d79-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="89d79-128">H:\Photo\\</span></span> |<span data-ttu-id="89d79-129">zdjęcie /</span><span class="sxs-lookup"><span data-stu-id="89d79-129">photo/</span></span>|
|<span data-ttu-id="89d79-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="89d79-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="89d79-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="89d79-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="89d79-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="89d79-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="89d79-133">Muzyka</span><span class="sxs-lookup"><span data-stu-id="89d79-133">music</span></span>|

<span data-ttu-id="89d79-134">Do tego mapowania hello pliku `H:\Video\Drama\GreatMovie.mov` będzie toohello importowanych obiektów blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="89d79-134">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="89d79-135">Określenie wymagań dotyczących dysku twardego</span><span class="sxs-lookup"><span data-stu-id="89d79-135">Determine hard drive requirements</span></span>

<span data-ttu-id="89d79-136">Następnie toodetermine liczbę dysków twardych są potrzebne, obliczeń hello rozmiar danych hello:</span><span class="sxs-lookup"><span data-stu-id="89d79-136">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="89d79-137">Na przykład dwa 8TB dyski twarde powinny być wystarczające.</span><span class="sxs-lookup"><span data-stu-id="89d79-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="89d79-138">Jednak ponieważ katalog źródłowy hello `H:\Video` ma 12TB danych i pojemności pojedynczego dysku twardego w tylko 8TB, będziesz w stanie toospecify to w hello w następujący sposób w hello **driveset.csv** pliku:</span><span class="sxs-lookup"><span data-stu-id="89d79-138">However, since hello source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able toospecify this in hello following way in hello **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="89d79-139">Narzędzie Hello będzie rozpowszechniają danych dwóch dysków twardych w sposób zoptymalizowane.</span><span class="sxs-lookup"><span data-stu-id="89d79-139">hello tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-hello-job"></a><span data-ttu-id="89d79-140">Dołącz dysków i skonfigurować zadanie hello</span><span class="sxs-lookup"><span data-stu-id="89d79-140">Attach drives and configure hello job</span></span>
<span data-ttu-id="89d79-141">Zostanie Dołącz zarówno maszyny toohello dysków i tworzyć woluminów.</span><span class="sxs-lookup"><span data-stu-id="89d79-141">You will attach both disks toohello machine and create volumes.</span></span> <span data-ttu-id="89d79-142">Następnie tworzyć **dataset.csv** pliku:</span><span class="sxs-lookup"><span data-stu-id="89d79-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="89d79-143">Ponadto można ustawić hello następujące metadane dla wszystkich plików:</span><span class="sxs-lookup"><span data-stu-id="89d79-143">In addition, you can set hello following metadata for all files:</span></span>

* <span data-ttu-id="89d79-144">**UploadMethod:** usługi Import/Eksport systemu Windows Azure</span><span class="sxs-lookup"><span data-stu-id="89d79-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="89d79-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="89d79-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="89d79-146">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="89d79-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="89d79-147">metadane tooset plików hello zaimportowane, Utwórz plik tekstowy `c:\WAImportExport\SampleMetadata.txt`, z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="89d79-147">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="89d79-148">Można również ustawić niektórych właściwości hello `FavoriteMovie.ISO` obiektu blob:</span><span class="sxs-lookup"><span data-stu-id="89d79-148">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="89d79-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="89d79-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="89d79-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==</span><span class="sxs-lookup"><span data-stu-id="89d79-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="89d79-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="89d79-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="89d79-152">tooset te właściwości, Utwórz plik tekstowy `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="89d79-152">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="89d79-153">Uruchom hello Azure narzędzie importu/eksportu (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="89d79-153">Run hello Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="89d79-154">Teraz wszystko jest gotowe toorun hello Azure narzędzie importu/eksportu tooprepare hello dwóch dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="89d79-154">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span>

<span data-ttu-id="89d79-155">**Dla hello pierwszej sesji:**</span><span class="sxs-lookup"><span data-stu-id="89d79-155">**For hello first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="89d79-156">Jeśli więcej danych wymaga toobe dodany, należy utworzyć inny plik zestawu danych (tego samego formatu co Initialdataset).</span><span class="sxs-lookup"><span data-stu-id="89d79-156">If any more data needs toobe added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="89d79-157">**Dla hello drugiej sesji:**</span><span class="sxs-lookup"><span data-stu-id="89d79-157">**For hello second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="89d79-158">Po hello kopiowania sesji została ukończona, można odłączyć Witaj dwie stacje z komputera kopiowania hello i wysłać je toohello centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="89d79-158">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Azure data center.</span></span> <span data-ttu-id="89d79-159">Będzie przekazać hello dwa pliki dziennika, `<FirstDriveSerialNumber>.xml` i `<SecondDriveSerialNumber>.xml`, podczas tworzenia zadania importu hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="89d79-159">You'll upload hello two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create hello import job in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89d79-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89d79-160">Next steps</span></span>

* [<span data-ttu-id="89d79-161">Przygotowywanie dysków twardych do zadania importu</span><span class="sxs-lookup"><span data-stu-id="89d79-161">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="89d79-162">Krótki przewodnik dla często używanych poleceń</span><span class="sxs-lookup"><span data-stu-id="89d79-162">Quick reference for frequently used commands</span></span>](../storage-import-export-tool-quick-reference.md)
