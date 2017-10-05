---
title: "Przykładowy przepływ pracy do przygotowywanie dyski twarde dla zadania importu Import/Eksport Azure | Dokumentacja firmy Microsoft"
description: "Zobacz Przewodnik ukończenia procesu przygotowywania dysków dla zadania importu w usłudze Import/Eksport Azure."
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
ms.openlocfilehash: 83cb82b9807718e7a509312d159eb766a5da1d2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="cf862-103">Przykładowy przepływ pracy przygotowywania dysków twardych do zadania importu</span><span class="sxs-lookup"><span data-stu-id="cf862-103">Sample workflow to prepare hard drives for an import job</span></span>

<span data-ttu-id="cf862-104">W tym artykule przedstawiono Zakończ proces przygotowywania dysków dla zadania importu.</span><span class="sxs-lookup"><span data-stu-id="cf862-104">This article walks you through the complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="cf862-105">Dane przykładowe</span><span class="sxs-lookup"><span data-stu-id="cf862-105">Sample data</span></span>

<span data-ttu-id="cf862-106">W tym przykładzie importuje następujące dane do konta magazynu platformy Azure o nazwie `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="cf862-106">This example imports the following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="cf862-107">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="cf862-107">Location</span></span>|<span data-ttu-id="cf862-108">Opis</span><span class="sxs-lookup"><span data-stu-id="cf862-108">Description</span></span>|<span data-ttu-id="cf862-109">Rozmiar danych</span><span class="sxs-lookup"><span data-stu-id="cf862-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="cf862-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="cf862-110">H:\Video\\</span></span> |<span data-ttu-id="cf862-111">Kolekcja filmów wideo</span><span class="sxs-lookup"><span data-stu-id="cf862-111">A collection of videos</span></span>|<span data-ttu-id="cf862-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="cf862-112">12 TB</span></span>|
|<span data-ttu-id="cf862-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="cf862-113">H:\Photo\\</span></span> |<span data-ttu-id="cf862-114">Kolekcja zdjęć</span><span class="sxs-lookup"><span data-stu-id="cf862-114">A collection of photos</span></span>|<span data-ttu-id="cf862-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="cf862-115">30 GB</span></span>|
|<span data-ttu-id="cf862-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="cf862-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="cf862-117">Obraz dysku A Blu-ray™</span><span class="sxs-lookup"><span data-stu-id="cf862-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="cf862-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="cf862-118">25 GB</span></span>|
|<span data-ttu-id="cf862-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="cf862-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="cf862-120">Kolekcja plików muzycznych w udziale sieciowym</span><span class="sxs-lookup"><span data-stu-id="cf862-120">A collection of music files on a network share</span></span>|<span data-ttu-id="cf862-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="cf862-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="cf862-122">Miejsca docelowe konto magazynu</span><span class="sxs-lookup"><span data-stu-id="cf862-122">Storage account destinations</span></span>

<span data-ttu-id="cf862-123">Zadania importu będzie importowanie danych do następujących miejsc docelowych na koncie magazynu:</span><span class="sxs-lookup"><span data-stu-id="cf862-123">The import job will import the data into the following destinations in the storage account:</span></span>

|<span data-ttu-id="cf862-124">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="cf862-124">Source</span></span>|<span data-ttu-id="cf862-125">Katalog wirtualny docelowego lub obiektu blob</span><span class="sxs-lookup"><span data-stu-id="cf862-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="cf862-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="cf862-126">H:\Video\\</span></span> |<span data-ttu-id="cf862-127">wideo /</span><span class="sxs-lookup"><span data-stu-id="cf862-127">video/</span></span>|
|<span data-ttu-id="cf862-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="cf862-128">H:\Photo\\</span></span> |<span data-ttu-id="cf862-129">zdjęcie /</span><span class="sxs-lookup"><span data-stu-id="cf862-129">photo/</span></span>|
|<span data-ttu-id="cf862-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="cf862-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="cf862-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="cf862-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="cf862-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="cf862-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="cf862-133">Muzyka</span><span class="sxs-lookup"><span data-stu-id="cf862-133">music</span></span>|

<span data-ttu-id="cf862-134">Z tego mapowania pliku `H:\Video\Drama\GreatMovie.mov` zostaną zaimportowane do obiektu blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="cf862-134">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="cf862-135">Określenie wymagań dotyczących dysku twardego</span><span class="sxs-lookup"><span data-stu-id="cf862-135">Determine hard drive requirements</span></span>

<span data-ttu-id="cf862-136">Następnie aby ustalić, ile dyski twarde są potrzebne, obliczeń rozmiar danych:</span><span class="sxs-lookup"><span data-stu-id="cf862-136">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="cf862-137">Na przykład dwa 8TB dyski twarde powinny być wystarczające.</span><span class="sxs-lookup"><span data-stu-id="cf862-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="cf862-138">Jednak ponieważ katalog źródłowy `H:\Video` ma 12TB danych i pojemności pojedynczego dysku twardego w tylko 8TB, można określić w poniższy sposób w **driveset.csv** pliku:</span><span class="sxs-lookup"><span data-stu-id="cf862-138">However, since the source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able to specify this in the following way in the **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="cf862-139">Narzędzie będzie rozpowszechniają danych dwóch dysków twardych w sposób zoptymalizowane.</span><span class="sxs-lookup"><span data-stu-id="cf862-139">The tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-the-job"></a><span data-ttu-id="cf862-140">Dołącz dysków i skonfigurować zadania</span><span class="sxs-lookup"><span data-stu-id="cf862-140">Attach drives and configure the job</span></span>
<span data-ttu-id="cf862-141">Zostanie Dołącz obydwa dyski do maszyny i tworzyć woluminów.</span><span class="sxs-lookup"><span data-stu-id="cf862-141">You will attach both disks to the machine and create volumes.</span></span> <span data-ttu-id="cf862-142">Następnie tworzyć **dataset.csv** pliku:</span><span class="sxs-lookup"><span data-stu-id="cf862-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="cf862-143">Ponadto można ustawić następujące metadane dla wszystkich plików:</span><span class="sxs-lookup"><span data-stu-id="cf862-143">In addition, you can set the following metadata for all files:</span></span>

* <span data-ttu-id="cf862-144">**UploadMethod:** usługi Import/Eksport systemu Windows Azure</span><span class="sxs-lookup"><span data-stu-id="cf862-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="cf862-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="cf862-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="cf862-146">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="cf862-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="cf862-147">Aby ustawić metadane dla importowanych plików, Utwórz plik tekstowy `c:\WAImportExport\SampleMetadata.txt`, o następującej treści:</span><span class="sxs-lookup"><span data-stu-id="cf862-147">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="cf862-148">Można również ustawić niektórych właściwości `FavoriteMovie.ISO` obiektu blob:</span><span class="sxs-lookup"><span data-stu-id="cf862-148">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="cf862-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="cf862-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="cf862-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==</span><span class="sxs-lookup"><span data-stu-id="cf862-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="cf862-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="cf862-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="cf862-152">Aby ustawić te właściwości, należy utworzyć plik tekstowy `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="cf862-152">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-the-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="cf862-153">Uruchom narzędzie Azure importu/eksportu (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="cf862-153">Run the Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="cf862-154">Teraz można przystąpić do uruchomienia narzędzia importu/eksportu Azure przygotować dwóch dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="cf862-154">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span>

<span data-ttu-id="cf862-155">**Podczas pierwszej sesji:**</span><span class="sxs-lookup"><span data-stu-id="cf862-155">**For the first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="cf862-156">Jeśli więcej danych musi zostać dodany, należy utworzyć inny plik zestawu danych (tego samego formatu co Initialdataset).</span><span class="sxs-lookup"><span data-stu-id="cf862-156">If any more data needs to be added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="cf862-157">**Dla drugiego sesji:**</span><span class="sxs-lookup"><span data-stu-id="cf862-157">**For the second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="cf862-158">Po sesji kopiowania została ukończona, można odłączyć dwóch dysków z komputera, kopiowania i wysyłać je do centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="cf862-158">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Azure data center.</span></span> <span data-ttu-id="cf862-159">Będzie przekazać pliki dziennika dwóch `<FirstDriveSerialNumber>.xml` i `<SecondDriveSerialNumber>.xml`, podczas tworzenia zadania importu w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cf862-159">You'll upload the two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create the import job in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf862-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cf862-160">Next steps</span></span>

* [<span data-ttu-id="cf862-161">Przygotowywanie dysków twardych do zadania importu</span><span class="sxs-lookup"><span data-stu-id="cf862-161">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="cf862-162">Krótki przewodnik dla często używanych poleceń</span><span class="sxs-lookup"><span data-stu-id="cf862-162">Quick reference for frequently used commands</span></span>](../storage-import-export-tool-quick-reference.md)
